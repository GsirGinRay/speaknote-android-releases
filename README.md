# SpeakNote 手機鍵盤（Android）安裝檔

這個 repo **只放 SpeakNote Android 鍵盤的安裝檔（APK）**，不放程式碼。

## 下載與安裝

1. 到 [Releases](https://github.com/GsirGinRay/speaknote-android-releases/releases/latest) 下載最新版的 `SpeakNoteKeyboard-x.y.z-arm64-v8a.apk`（支援 arm64 手機，例如三星 S24 Ultra）。
2. 每個版本都附一個 `.sha256` 檔，可以用來核對下載的檔案有沒有損壞或被換掉。
3. 已經裝過 0.1.3 以後的版本，App 會自己檢查新版，跳出「更新」按鈕，不用再手動下載。

## 安全與隱私

- 語音辨識、注音與英文打字都在手機上完成，**不會把打的字或錄音傳出去**。
- App 只會連到 GitHub，用來檢查和下載新版本，不會帶任何帳號或金鑰。
- 每個 APK 都用同一把簽章金鑰簽署。Android 只接受同一把金鑰簽的更新，簽章不同的檔案無法覆蓋安裝。

## 第三方元件

| 元件 | 授權 |
|---|---|
| [libchewing](https://github.com/chewing/libchewing)（注音引擎） | LGPL-2.1-or-later |
| [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx)（語音辨識 runtime） | Apache-2.0 |
| [ONNX Runtime](https://github.com/microsoft/onnxruntime) | MIT |
| SenseVoiceSmall by FunASR / FunAudioLLM（[模型說明](https://github.com/FunAudioLLM/SenseVoice)），使用 sherpa-onnx 的 int8 轉換版 `sherpa-onnx-sense-voice-zh-en-ja-ko-yue-int8-2024-07-17` | [FunASR Model License v1.1](https://github.com/modelscope/FunASR/blob/main/MODEL_LICENSE) |
| [OpenCC](https://github.com/BYVoid/OpenCC) 對照表 | Apache-2.0 |