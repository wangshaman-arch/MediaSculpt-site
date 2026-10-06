# MediaSculpt V0.860 Windows 基础安装包

> Windows 公开测试预览 · 受限基础安装包 · **不是源代码发布包**

本页只发布可直接安装的 Windows 受限基础版安装器；发布页不提供任何源代码或源码压缩包。普通用户请下载并运行 `.exe` 安装器。

## 下载

- [下载 Windows 基础预览安装器](https://github.com/wangshaman-arch/MediaSculpt-site/releases/download/v0.860.0/MediaSculpt_0.860.0_x64-setup-base.exe)
- [下载安装器 SHA-256](https://github.com/wangshaman-arch/MediaSculpt-site/releases/download/v0.860.0/MediaSculpt_0.860.0_x64-setup-base.exe.sha256)

本版本提供受限基础安装包，大小约 162 MB，文件版本为 `0.860.0`。它包含原生桌面窗口、本地 API、Node.js、FFmpeg/FFprobe 和 HandBrakeCLI；Whisper、OCR、翻译工具和模型按需安装。安装包不是源代码，也不要求用户先安装 Node.js 或 pnpm。

## 本次内容

- 工具链下载更可靠：刷新 GitHub 加速镜像列表（只保留实测可用者），为 Whisper 模型增加 ModelScope 备用镜像，并为 HandBrake、Tesseract、7-Zip 加入 SHA-256 校验。
- 来源目录默认按“修改时间”倒序（新文件与文件夹在上），可随时切换回按名称排序。
- 在“设置与预览”完成确认后直接进入任务队列，不再停留在预览环节。
- 任务队列页合并为单一滚动条；“源预览与处理设置”对话框适配默认窗口尺寸，不再溢出或贴边。
- 字幕：OCR 双语纠错结果不再被通用翻译二次覆盖；OCR 纠错调用遵循已配置的 AI 代理。
- 任务回收更安全：只回收确实仍在运行且子进程已消失的任务，避免误改已完成任务。
- 仅用环境变量注入 AI Key 时，界面不再误判为不可用。
- 移除未使用组件并精简模块，改善可维护性。

## 构建 Windows 基础安装器

在内存充足的 Windows 开发机上运行：

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\build-tauri-base.ps1
```

生成的文件位于 `release\MediaSculpt_0.860.0_x64-setup-base.exe`，并有同名 `.sha256` 校验文件。发布页中的安装器就是按此脚本、当前 `V0.860` 版本和 `preview` 受限模式生成的版本。

## 已验证项目

- 类型检查通过（scripts、api-server、video-agent）。
- API 测试：119 个测试文件、834 项通过。
- 前端测试：46 个测试文件、177 项通过。
- 前端生产构建通过；仅保留已有的 sourcemap 与 bundle 大小提示。
- Playwright 布局冒烟测试：9 项通过（默认窗口、最小窗口、高 DPI）。
- Tauri NSIS 基础安装器构建通过，文件版本 `0.860.0`，大小约 162.48 MB，并输出同名 `.sha256` 校验文件。

## 测试边界

真实 DVD/蓝光测试必须在本机工具状态正常、源盘可读且输出目录可写的环境中进行。本版本只修复并验证本次改动，不宣称所有不规范光盘都已解决。预览版使用 30 天或 20 次成功主任务限制，以先到者为准。
