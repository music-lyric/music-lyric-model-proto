# music-lyric-model-proto

[English](./README.md) | [简体中文](./README.zh-Hans.md) | [繁體中文](./README.zh-Hant.md)

**music lyric model** 的 Protobuf schema.

## 目录结构

```
src/
  info.proto              # Info, 根消息
  common/time.proto
  meta/meta.proto
  agent/agent.proto
  language/language.proto
  line/content.proto      # Line 及其变体
  line/annotation.proto
  word/content.proto      # Word 及其变体
  word/annotation.proto
```

所有类型均定义于 `lyric` package 下, import 路径以 `src/` 为根 (例如 `import "common/time.proto";`).

## 版本

schema 以 git tag `vX.Y.Z` 发布; tag 即版本号, 因此仓库中不另行保存版本文件. 各绑定从其所 pin 的 tag 读取版本.

- **major**: wire 上的破坏性变更
- **minor**: 增量变更 (新增字段, 消息或枚举值)
- **patch**: 不影响 wire 的变更 (文档, 注释等)

该版本号通过 wire 写入 `Info.version`.

## 使用

在绑定仓库中将本仓库作为 submodule 引入, 并 pin 到指定的发布 tag:

```bash
git submodule add https://github.com/music-lyric/music-lyric-model-proto.git proto
git -C proto checkout v1.0.0
```

随后使用自有的 `buf` 或 `protoc` 生成代码, import 根目录指向 `proto/src`.

## 工具

`buf.yaml` 用于定义模块, 并提供 `buf lint` 与 `buf breaking`; 后者用于保障 wire 兼容性. 代码生成由各绑定负责, 不在本仓库进行.
