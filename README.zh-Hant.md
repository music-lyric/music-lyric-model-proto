# music-lyric-model-proto

[English](./README.md) | [简体中文](./README.zh-Hans.md) | [繁體中文](./README.zh-Hant.md)

**music lyric model** 的 Protobuf schema.

## 目錄結構

```
src/
  version.txt             # 規範版本號
  info.proto              # Info, 根訊息
  common/time.proto
  meta/meta.proto
  agent/agent.proto
  language/language.proto
  line/content.proto      # Line 及其變體
  line/annotation.proto
  word/content.proto      # Word 及其變體
  word/annotation.proto
```

所有型別均定義於 `lyric` package 下, import 路徑以 `src/` 為根 (例如 `import "common/time.proto";`).

## 版本

規範版本號保存於 `src/version.txt`, 並以同名 git tag `vX.Y.Z` 發佈. 各綁定會從其所 pin 的 tag 對應的該檔案讀取版本.

- **major**: wire 上的破壞性變更
- **minor**: 增量變更 (新增欄位, 訊息或列舉值)
- **patch**: 不影響 wire 的變更 (文件, 註解等)

該版本號透過 wire 寫入 `Info.version`.

## 使用

在綁定儲存庫中將本儲存庫作為 submodule 引入, 並 pin 到指定的發佈 tag:

```bash
git submodule add https://github.com/music-lyric/music-lyric-model-proto.git proto
git -C proto checkout v1.0.0
```

隨後使用自有的 `buf` 或 `protoc` 產生程式碼, import 根目錄指向 `proto/src`.

## 工具

`buf.yaml` 用於定義模組, 並提供 `buf lint` 與 `buf breaking`; 後者用於保障 wire 相容性. 程式碼產生由各綁定負責, 不在本儲存庫進行.
