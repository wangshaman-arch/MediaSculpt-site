# MediaSculpt 第三方组件说明

> **Version:** V 0.850 · 版本：V 0.850

MediaSculpt 本身是专有软件。下列组件可能随 Windows 基础安装器提供，或由软件工具管理器按用户选择下载和管理；它们各自适用原许可证。

## 当前运行时组件

- Tauri 2：桌面窗口和原生宿主，Apache-2.0 / MIT。
- Node.js：本地 API 侧车运行时，MIT license。
- React、Vite、TypeScript 及 JavaScript 依赖：依各自许可证执行。
- FFmpeg / FFprobe：本地媒体探测、提取、无损封装和转码；实际分发二进制须保留相应许可证说明。
- HandBrakeCLI：本地视频压缩；按其 GPLv2 及随包许可证说明执行。
- Whisper / faster-whisper、Tesseract OCR、RapidOCR 和语言数据：按各自运行时、模型和数据包许可证执行。

发布具体安装器时，应对实际打入安装器的二进制、模型、语言数据和依赖生成逐项清单，并保留对应许可证文件。

