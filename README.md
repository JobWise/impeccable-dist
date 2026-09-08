# impeccable-dist

The Impeccable skill payload, vendored once for all JobWise repos. Consumer
repos reference this as a git submodule (conventionally at `vendor/impeccable`)
and commit two symlinks:

    .claude/skills/impeccable -> ../../vendor/impeccable/claude
    .agents/skills/impeccable -> ../../vendor/impeccable/codex

Clone consumers with `git clone --recurse-submodules`; after a plain clone or
in a new worktree, run `git submodule update --init`.

## Updating the payload

1. In this repo: `npx impeccable update` (writes claude/ and codex/), then
   copy the refreshed `.impeccable/upstream.json` here as `upstream.json`.
2. Commit and push with the payload version in the message.
3. In each consumer: bump the submodule SHA, sync `.impeccable/upstream.json`
   from `vendor/impeccable/upstream.json`, and run the repo's validator (it
   SHA-256-verifies the linked trees against upstream.json).

Payload version and provenance: see `upstream.json`. License: Apache-2.0
(see `claude/` payload for LICENSE terms carried from upstream).
