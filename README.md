# impeccable-dist

The Impeccable skill payload, vendored once for all JobWise repos. Consumer
repos reference this as a git submodule (conventionally at `vendor/impeccable`)
and commit two symlinks:

    .claude/skills/impeccable -> ../../vendor/impeccable/claude
    .agents/skills/impeccable -> ../../vendor/impeccable/codex

Clone consumers with `git clone --recurse-submodules`; after a plain clone or
in a new worktree, run `git submodule update --init`.

## Updating the payload

Run `npm run update-impeccable` in paper-doll. The updater only detects real
harness installs, so the update runs in a consumer and its writes land through
the symlinks into this repo's working copy; the script then commits and pushes
here, syncs `upstream.json`, bumps the consumer's submodule pointer, and
validates (SHA-256 verification of the linked trees).

Additional consumers afterwards: bump the submodule SHA and sync
`.impeccable/upstream.json` from `vendor/impeccable/upstream.json`.

Update deliberately — when release notes matter or a bug bites — not on a
timer. The pin is a feature.

Payload version and provenance: see `upstream.json`. License: Apache-2.0
(see `claude/` payload for LICENSE terms carried from upstream).
