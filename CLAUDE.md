# image/debian — signpost (not the rule-set)

This submodule is the **Debian** base image family: an `charly.yml` (plus
per-kind sibling files) that imports the main repo under the `charly` namespace and `build.yml` flat.

**Load these skills FIRST (R0):**

- `/charly-distros:debian` — the Debian 13 base image (uid-1000 create mode).
- `/charly-distros:debian-builder` — the builder image.
- `/charly-distros:debian-debootstrap`, `/charly-distros:debian-debootstrap-builder` —
  the bootstrap path.
- `/charly-coder:debian-coder` — the dev image; `/charly-vm:debian` — the bootstrap VM.

**Authoritative rules live in the `opencharly` superproject's root `CLAUDE.md`**
(R0–R10, hard-cutover, AI attribution, git-workflow). This file only signposts
and restates no rule. The multi-agent workflow is in `/charly-internals:agents`.
History lives in `CHANGELOG.md`.
