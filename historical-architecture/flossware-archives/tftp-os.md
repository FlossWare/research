# tftp-os: Engineering Research

**Source:** `FlossWare-Archives/tftp-os`

**Status:** Historical research / resurrection candidate

**Source status:** Public, archived repository. The repository describes itself as a reusable TFTP-based firmware provisioning foundation and explicitly positions `pxe-os` as a higher-level decorator/application layer.

## Executive summary

tftp-os is more interesting than its name suggests. Its core abstraction is not TFTP itself. It is a **device-to-provisioning-resolution engine** that maps identity and context (MAC, hostname, subnet, serial, group, architecture) to a provisioning profile and then to a firmware artifact through a plugin registry.

The important conceptual pipeline is:

```text
request identity/context
        ↓
    HostMatcher
        ↓
   HostRule
        ↓
ProvisionProfile
        ↓
  PluginRegistry
        ↓
 FirmwarePlugin
        ↓
 firmware path
        ↓
 optional staging
        ↓
 external TFTP server
```

This is deliberately separated from the TFTP protocol. The repository explicitly states that tftp-os resolves and stages firmware but does not speak TFTP, allowing it to pair with dnsmasq, tftpd-hpa, atftpd, or another server.

## Core architectural ideas

### 1. Identity/context resolution is the real core

`HostMatcher` supports ordered matching tiers:

1. exact MAC
2. MAC prefix
3. hostname pattern
4. subnet
5. serial
6. group
7. architecture
8. catch-all

Within a tier, explicit priority breaks ties. The matcher therefore acts as a small deterministic policy engine rather than merely doing dictionary lookup.

This abstraction is reusable well beyond firmware provisioning: any system that needs to map an incoming identity/context tuple to a policy/profile can use the same pattern.

### 2. Separate policy from artifact generation

The `FirmwareEngine` does not itself know how firmware is laid out. It resolves a rule, loads a profile, asks the registry for the plugin corresponding to `os_family`, validates the profile, and delegates artifact-path selection to the plugin.

That is a strong separation:

```text
matching policy ≠ provisioning profile ≠ artifact implementation
```

### 3. Plugin registry is an extension boundary

`PluginRegistry` supports direct registration, entry-point discovery, and local module discovery. `FirmwarePlugin` is the stable abstraction around firmware families.

This allows third-party firmware handlers without modifying the core engine. The `pyproject.toml` also exposes `tftpos.plugins` as the entry-point namespace and registers built-in static/OpenWrt plugins.

### 4. Provisioning is modeled as a state machine

The project tracks:

```text
REGISTERED → BOOTING → INSTALLING → POST_INSTALL → COMPLETE
                                      └──────────→ FAILED
```

`ProvisionRecord` preserves timestamps, state history, error information, and boot-once/netboot state. `ProvisionTracker` supports callbacks and optional persistence through a storage backend.

This is an important operational insight: provisioning is treated as a **long-running lifecycle**, not merely a file lookup.

### 5. Core library vs. application layer is explicitly considered

`docs/SCOPE.md` records a deliberate attempt to separate core firmware resolution from higher-level concerns. The documented core includes engine, matcher, registry, config, models, state, database abstraction, validation, staging, and plugin base/static implementation.

Other capabilities such as webhooks, Prometheus metrics, audit, console access, power management, cloud-init, cluster provisioning, and hypervisor lifecycle are explicitly classified as extended or application-layer candidates.

This separation is one of the most valuable architectural lessons in the repository.

## Interesting historical engineering decisions

- TOML is used for configuration, host rules, and provisioning profiles.
- SQLAlchemy provides the persistence abstraction, with SQLite as the simple default and PostgreSQL/MySQL support available through extras.
- The package targets Python 3.10+ and uses type checking, Ruff, pytest, coverage, Bandit, and mypy configuration.
- Profile loading is cached with a bounded TTL cache.
- Profile-name handling includes path traversal protection before loading from the profile directory.
- Staging is separate from firmware resolution and can use symlinks.
- The project has a lab proof for the MAC → stage → TFTP transfer → checksum verification path while explicitly acknowledging that it has not been deployed in production.
- The repository reports 1,072 passing tests at the archived snapshot, which is notable for an Alpha systems library.

## Scope evolution

The scope document records multi-model architectural review and subsequent issue-driven restructuring. The important lesson is not the model voting itself. It is that the project recognized **scope creep around a small core** and attempted to establish explicit ownership boundaries.

The intended ecosystem is:

```text
                    tftp-os
               firmware foundation
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
          pxe-os          application layers
       OS provisioning      / integrations
```

`pxe-os` is described as adding iPXE generation, installer templates, OS installer plugins, DHCP configuration, and a web UI.

## Research findings

### Finding A: The name hides a generic policy engine

The most reusable idea is not TFTP. It is the combination of:

```text
identity/context → ordered matching → named profile → plugin → artifact
```

This resembles a small policy-resolution runtime and could be useful in many provisioning and infrastructure systems.

### Finding B: Explicit match tiers are preferable to accidental precedence

The matcher makes precedence visible in code rather than relying solely on configuration ordering. That is a useful pattern whenever multiple selectors can overlap.

### Finding C: Lifecycle state deserves first-class modeling

Provisioning state, history, timestamps, callbacks, persistence, and boot-once behavior are modeled explicitly. Systems that begin as simple request/response services often become operationally difficult when lifecycle state is bolted on later. tftp-os puts it near the core.

### Finding D: The repository recognized the danger of becoming a monolith

The explicit scope analysis and migration candidates show awareness that a reusable foundation should not absorb every feature adjacent to its domain. The distinction between library and application layer is particularly valuable historical evidence.

### Finding E: External protocol separation is strong architecture

Not speaking TFTP is a feature, not a missing feature. The library resolves and stages artifacts while an existing protocol server performs transport. That keeps the core smaller and permits multiple deployment environments.

## Resurrection assessment

**High-value resurrection candidate.**

Before production use, a resurrection should start with the core rather than immediately carrying forward every module. The first investigation should focus on:

1. `HostMatcher`
2. models and configuration
3. `FirmwareEngine`
4. plugin contract/registry
5. staging
6. provisioning state and persistence
7. security/validation boundaries
8. lab proof and integration behavior

Then evaluate whether extended modules belong in tftp-os at all or should remain in `pxe-os`, `flossware-tftp-os`, or a future infrastructure application.

## Provenance

Primary evidence reviewed from the public archived repository:

- `README.md`
- `docs/SCOPE.md`
- `pyproject.toml`
- `tftpos/engine.py`
- `tftpos/matcher.py`
- `tftpos/registry.py`
- `tftpos/state.py`

This document is derived research, not a claim that every historical implementation detail has been reviewed. Further source review should refine or correct these findings.
