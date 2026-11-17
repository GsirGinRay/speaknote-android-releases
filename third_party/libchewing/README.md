# libchewing 原始碼（LGPL-2.1-or-later）

SpeakNote 手機鍵盤裡的 `libchewing_jni.so` 由 **libchewing 0.9.1** 和一層 JNI 包裝一起編成，整個 .so 以 LGPL-2.1-or-later 授權。依 LGPL，這裡提供對應的完整原始碼與建置說明，任何人都可以修改 libchewing 後重新編出這個 .so 換進 App。

## 檔案

| 檔案 | 內容 | SHA-256 |
|---|---|---|
| `libchewing-0.9.1-bab0250.tar.gz` | libchewing 官方 v0.9.1（commit `bab025039a24d610d5c327d6894356a3d645e441`），**未修改**。上游：https://github.com/chewing/libchewing | `7577e39e37a2138235034017e269cfb5bd91a96e86e329327a90b4a9b592e4cc` |
| `speaknote-chewing-jni-src-1627951.tar.gz` | JNI 包裝（`native/chewing-jni`）、詞庫建置工具（`native/chewing-dictgen`）、追加詞表（`native/chewing-extra`）、首注音索引產生器（`tools/gen_abbrev_index.py`）與交叉編譯腳本（`tools/build_chewing_jni.ps1`） | `cfb3c3a6a90eecccacb066815f018942078f67363e286642604d4326ab95b31e` |
| `COPYING` | GNU LGPL 2.1 全文 | |

## 適用版本

- JNI 包裝自 0.1.2 起未變更，上面的包裝原始碼適用於 0.1.2、0.1.3、0.1.4。
- libchewing 一律是未修改的 0.9.1。
- `tsi.dat`／`word.dat` 詞庫由 libchewing 0.9.1 的 `data/tsi.src`、`data/word.src` 以 `chewing-cli init-database -t trie` 產生；首注音索引 `assets/abbrev/index.bin` 由 `gen_abbrev_index.py` 從同一份資料加上 `native/chewing-extra` 產生。

## 重新建置 libchewing_jni.so（arm64-v8a）

需求：Rust（加 `aarch64-linux-android` target）、Android NDK 27.0.12077973。

1. 解開兩個壓縮檔，讓目錄結構成為 `<root>/third_party/libchewing`（libchewing 原始碼）與 `<root>/native/chewing-jni`（包裝），`Cargo.toml` 以相對路徑 `../../third_party/libchewing/capi` 引用 libchewing。
2. 可自行修改 libchewing。
3. 執行 `tools/build_chewing_jni.ps1`（或在 `native/chewing-jni` 下以 NDK 的 `aarch64-linux-android28-clang` 當 linker 執行 `cargo build --release --target aarch64-linux-android`，連結參數 `-Wl,-z,max-page-size=16384`）。
4. 用產出的 `libchewing_jni.so` 取代 APK 內 `lib/arm64-v8a/libchewing_jni.so`，重新 zipalign 並以你自己的金鑰簽署即可安裝（簽章不同時需先移除原 App）。

## 索取原始碼

若上面的連結失效，可在 https://github.com/GsirGinRay/speaknote-android-releases/issues 開 issue 索取，本提供自每個版本發佈起至少三年內有效。