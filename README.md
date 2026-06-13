# overthinkos/debian

The **Debian image family** for [OpenCharly](https://github.com/overthinkos/overthink),
split into its own repository and mounted as a git submodule at `box/debian`
of the main repo.

## What's here

| Kind | Entries |
|---|---|
| `image:` | `debian` (base), `debian-builder`, `debian-coder`, `debian-debootstrap`, `debian-debootstrap-builder` |
| `vm:` | `debian-debootstrap` (bootstrap-from-scratch via debootstrap) |
| `deploy:` | `check-debian-debootstrap-vm` (disposable bootstrap-VM bed) |

## Composition by reference — nothing is vendored

This repo contains **no layers and no build-config of its own**. Everything is
pulled from `github.com/overthinkos/overthink` by **github reference**:

- every layer in `box.yml` is an `@github.com/overthinkos/overthink/candy/<name>:<tag>` ref;
- the shared build-config (`build.yml` — distro/builder/init, including the
  `debian` distro definition, the `deb` format template, and the `debootstrap`
  builder template) is a remote `import:` in `charly.yml`.

The Debian bases root at the upstream docker.io `debian:13` image directly, so
this repo needs **no remote base include** (unlike `overthinkos/cachyos`, which
owns its base, or `overthinkos/arch`, which remote-includes `arch-base.yml`).
All references pin to a single tag of the upstream repo, so a build is
reproducible. There is exactly one definition of every layer — no duplication.

## No coupling with main

Nothing in the main `opencharly` repo consumes any Debian image (no
`base: debian` image stays in main), so there is **no main ↔ debian coupling**:
the only edge is `debian → main` (this repo pulls layers + `build.yml`). Main
pulls nothing back. The image DAG is acyclic
(`debian-coder → debian → docker.io/debian:13`;
`debian-debootstrap → debian-debootstrap-builder → docker.io/debian:13`).

## Build

```bash
# Inside the submodule (the build verb defaults to charly.yml):
charly box build debian

# From the parent opencharly repo:
charly -C box/debian box build debian

# Standalone, against the published repo:
charly --repo overthinkos/debian box build debian
```

The first build resolves the upstream github references into
`~/.cache/charly/repos/` and materializes the referenced layers under
`.build/_layers/`.

## debootstrap-from-scratch (`debian-debootstrap` / `check-debian-debootstrap-vm`)

`debian-debootstrap` builds a Debian rootfs from scratch via `debootstrap`
inside the privileged `debian-debootstrap-builder` container (`from:
builder:debootstrap`). `check-debian-debootstrap-vm` boots that rootfs under
libvirt/QEMU and carries `disposable: true`, so `charly -C box/debian update
check-debian-debootstrap-vm` rebuilds it unattended.

## Requirements

A build of any image here fetches from the upstream repo, so it needs network
access and a `charly` recent enough to understand the config's schema version
(`charly` hard-fails with an "update charly" message if the config is newer than the
binary supports).

---
*Assisted-by: Claude*
