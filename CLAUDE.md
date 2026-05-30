# image/debian — signpost (not the rule-set)

This submodule is the **Debian** base image family: a single `overthink.yml`
that imports the main repo under the `ov` namespace and `build.yml` flat.

**Load these skills FIRST (R0):**

- `/ov-distros:debian` — the Debian 13 base image (uid-1000 create mode).
- `/ov-distros:debian-builder` — the builder image.
- `/ov-distros:debian-debootstrap`, `/ov-distros:debian-debootstrap-builder` —
  the bootstrap path.
- `/ov-coder:debian-coder` — the dev image; `/ov-vm:debian` — the bootstrap VM.

**Authoritative rules live in the `overthink` superproject's root `CLAUDE.md`**
(R0–R10, hard-cutover, AI attribution, git-workflow). This file only signposts
and restates no rule. The multi-agent workflow is in `/ov-internals:agents`.
History lives in `CHANGELOG.md`.
