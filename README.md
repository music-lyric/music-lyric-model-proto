# music-lyric-model-proto

[English](./README.md) | [简体中文](./README.zh-Hans.md) | [繁體中文](./README.zh-Hant.md)

The Protobuf schema for the **music lyric model**.

## Layout

```
src/
  version.txt             # Canonical schema version
  info.proto              # Info — the root message
  common/time.proto
  meta/meta.proto
  agent/agent.proto
  language/language.proto
  line/content.proto      # Line and its variants
  line/annotation.proto
  word/content.proto      # Word and its variants
  word/annotation.proto
```

All types are defined in package `lyric`, with imports rooted at `src/` (e.g. `import "common/time.proto";`).

## Versioning

The canonical version is kept in `src/version.txt` and released as a matching git tag `vX.Y.Z`. Each binding reads the version from that file at the tag it pins.

- **major** — a breaking change on the wire
- **minor** — an additive change (a new field, message, or enum value)
- **patch** — a change that does not affect the wire (documentation, cosmetics)

The version is carried on the wire as `Info.version`.

## Usage

Add this repository as a submodule in your binding, pinned to a release tag:

```bash
git submodule add https://github.com/music-lyric/music-lyric-model-proto.git proto
git -C proto checkout v1.0.0
```

Then generate with your own `buf` or `protoc`, using `proto/src` as the import root.

## Tooling

`buf.yaml` defines the module and provides `buf lint` and `buf breaking`, the latter guarding wire compatibility. Code generation is performed in each binding, not here.
