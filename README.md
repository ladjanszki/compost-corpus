# compost-corpus

Test material for [compost](https://github.com/ladjanszki/compost), kept out of
the source tree on purpose.

The tool's repository carries a **smoke set** of about 80 KB — the few documents
its suites name directly, enough that every suite runs on a bare clone. This
repository carries the volume: the documents that make a green board mean
something.

Keeping them apart is a decision with a history. The tool's repo has twice had
material removed from its history retroactively, which is expensive and leaves
residue on any remote it was pushed to. Test data grows, and growth is exactly
what makes that removal expensive later. So it lives here from the start, and
nothing here has to be deleted from anywhere else if it turns out to be a
mistake.

## Layout

```
curated/
  edge-cases/   markdown and djot corner cases, written to break the reader
  notes/        longer prose documents
  sessions/     Claude Code transcripts, bleached — see below
```

Bulk material from other projects — the Rust book and similar — is **not** kept
here. It is fetched from upstream at a pinned commit, because a git commit SHA
already guarantees byte-identical content and republishing someone else's book
buys nothing.

## The sessions are bleached

Every string that could carry content has been replaced; everything that makes
a log work is untouched — line types, roles, block types, tool names, the
`uuid`/`parentUuid` chain, `tool_use_id` pairing, timestamps, sidechain flags.
Identifiers are remapped consistently, so the linkage graph is intact while the
identity is gone.

That is checked rather than eyeballed: `compost`'s `tests/test_bleach_session.py`
asserts the bleached log has the same line types, the same block types per
line, the same tool names and an isomorphic parent chain.

## How it is consumed

compost pins a commit of this repository and fetches it. Nothing here is
imported by path from the tool's source; the suites glob directories, so adding
a document here extends coverage without a code change.
