# MediaSculpt V0.856 Windows 基础安装包

> Windows 公开测试预览 · 受限基础安装包 · **不是源代码发布包**

本页发布对象是可直接安装的 Windows 基础版安装器，不是源码压缩包。源码预览包仅作为开发、复现和问题定位的辅助下载，普通用户应下载并运行 `.exe` 安装器。

## 下载

- [下载 Windows 基础预览安装器](https://github.com/wangshaman-arch/MediaSculpt-site/releases/download/v0.856.0/MediaSculpt_0.856.0_x64-setup-base.exe)
- [下载安装器 SHA-256](https://github.com/wangshaman-arch/MediaSculpt-site/releases/download/v0.856.0/MediaSculpt_0.856.0_x64-setup-base.exe.sha256)
- [下载源码预览包](https://wangshaman-arch.github.io/MediaSculpt-site/downloads/MediaSculpt-V0.856-preview-source.zip)
- [查看源代码仓库](https://github.com/wangshaman-arch/MediaSculpt)

本版本提供受限基础安装包，大小约 124 MB，文件版本为 `0.856.0`。它包含原生桌面窗口、本地 API、Node.js、FFmpeg/FFprobe 和 HandBrakeCLI；Whisper、OCR、翻译工具和模型按需安装。安装包不是源代码，也不要求用户先安装 Node.js 或 pnpm。源码预览包仅用于开发复现，不包含用户数据、数据库、日志或已下载工具。

## 本次内容

- 修复 DVD 源路径身份识别：支持 DVD 根目录、`VIDEO_TS`、`VTS_01_0.IFO`、BUP 和 VOB 路径。
- 单标题 DVD 不再把内部 `Title01` 错误写入输出名称；多标题仅在需要区分时保留标题身份。
- 统一 Remux、压缩和章节预览的 DVD 输出基名，避免同一张碟在不同入口生成不一致名称。
- 规范化 `11 Days 11 Nights Part 3 (1989) DVD` 等目录名，输出示例为 `11.Days.11.Nights.Part.3.1989.DVD.Remux.mkv`。
- 新增 DVD 源身份单元测试，并保留 API、前端和构建脚本。

## 源码开发（仅开发者）

1. Windows 10/11 64 位安装 Node.js `22.20.0+`、pnpm `9+`、Rust/Tauri 所需工具链。
2. 只有需要开发或复现问题时，才下载并解压 `MediaSculpt-V0.856-preview-source.zip`，进入解压目录。
3. 安装依赖：

   ```powershell
   pnpm install
   ```

4. 运行检查：

   ```powershell
   pnpm run typecheck
   pnpm run test:api -- --maxWorkers=1
   pnpm --filter @workspace/video-agent build
   ```

5. 普通用户不要按本节运行源码；普通使用请直接运行上面的 Windows 基础安装包。开发运行才使用根目录的 `Start MediaSculpt.bat`。

## 构建 Windows 基础安装器

在内存充足的 Windows 开发机上运行：

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\build-tauri-base.ps1
```

生成的文件位于 `release\MediaSculpt_0.856.0_x64-setup-base.exe`，并有同名 `.sha256` 校验文件。发布页中的安装器就是按此脚本、当前 `V0.856` 源码和 `preview` 受限模式生成的版本。

## 已验证项目

- DVD 源身份定向测试：3 个测试文件、28 个测试通过。
- API 类型检查通过。
- API 构建通过。
- 前端构建通过；仅保留已有的 sourcemap 和 bundle 大小提示。
- Tauri NSIS 基础安装器构建通过，文件版本 `0.856.0`，大小约 123.79 MB。

## 测试边界

真实 DVD/蓝光测试必须在本机工具状态正常、源盘可读且输出目录可写的环境中进行。本版本只修复并验证本次源码改动，不宣称所有不规范光盘都已解决。预览版使用 30 天或 20 次成功主任务限制，以先到者为准。
