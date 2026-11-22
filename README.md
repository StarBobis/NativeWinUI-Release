# 🪟 NativeWinUI

**轻量、原生、面向 Windows 桌面的 C++20 UI 框架。**

NativeWinUI 基于 Win32、Direct2D 和 DirectWrite，提供现代桌面控件、布局、主题与动画。本仓库提供预编译 SDK 和 Gallery 演示程序，下载后即可体验或接入 C++ 项目。

👉 [下载最新版本](https://github.com/StarBobis/NativeWinUI-Release/releases/latest) · [查看所有版本](https://github.com/StarBobis/NativeWinUI-Release/releases)

## ✨ 为什么选择 NativeWinUI？

- 🪶 **轻量交付**：原生 C++ 实现，核心 UI 无需捆绑浏览器引擎或 .NET 运行时；静态链接可由链接器裁去未使用的代码。实际体积见每个 Release 的附件大小。
- ⚡ **原生渲染路径**：使用 Direct2D / DirectWrite 绘制图形和文字，减少额外运行时层级；性能取决于页面复杂度、硬件和所用效果，不以未经测量的跑分作承诺。
- 🎨 **现代 Windows 风格**：支持明暗主题、主题资源、布局、焦点反馈、动画和丰富控件，可按应用需求组合界面。
- 🧩 **两种集成方式**：提供静态 LIB 和动态 DLL SDK，包含公开头文件及 CMake 接入配置。
- 🖥️ **Gallery 可直接体验**：交互查看按钮、输入框、导航、列表、弹出层、图形与动画等示例，内置中文与英文资源。
- 🧪 **便于验证**：支持无窗口逻辑测试、离屏渲染和自动化接口，减少 UI 回归验证对桌面的占用。

NativeWinUI 是独立实现的 UI 框架，并非微软 WinUI 3 的二进制替代品；可用能力及效果以当前 Gallery 和公开 API 为准。

## 📦 下载哪个文件？

| 附件 | 用途 |
| --- | --- |
| `NativeWinUI-版本号-win-x64-lib.zip` | 静态库 SDK：公开头文件、`NativeWinUI.lib`、CMake 配置、使用说明及许可证 |
| `NativeWinUI-版本号-win-x64-dll.zip` | 动态库 SDK：公开头文件、`NativeWinUI.dll`、导入库、CMake 配置、使用说明及许可证 |
| `NativeWinUIGallary.exe` | Gallery 演示程序，语言资源内嵌；直接运行即可体验 |
| `SHA256SUMS.txt` | 附件 SHA-256 校验值 |
| `release-manifest.json` | 版本、源码状态、工具链、构建退出码与验收记录 |
| `THIRD_PARTY_NOTICES.txt` | Gallery 及 SDK 使用的第三方许可证说明 |

> 文件名沿用项目现有拼写 `NativeWinUIGallary.exe`。

## 🚀 快速开始

**运行 Gallery**：下载 `NativeWinUIGallary.exe` 后启动。当前发布面向 Windows 10/11 x64；部分系统材质、合成能力和效果依赖系统版本及图形环境，系统相关效果可能回退。运行程序需要 Microsoft Visual C++ 2015–2022 x64 运行库。

**接入 SDK**：使用 MSVC v143、C++20、x64、Release 和 `/MD` 运行库。SDK 不承诺跨编译器或跨版本的 C++ ABI 兼容；请让头文件、LIB 和 DLL 来自同一版本。

解压任一 SDK，然后在工程中使用：

```cmake
cmake_minimum_required(VERSION 3.26)
project(MyApp LANGUAGES CXX)
find_package(NativeWinUI CONFIG REQUIRED)
add_executable(MyApp main.cpp)
target_link_libraries(MyApp PRIVATE NativeWinUI::UI)
```

```powershell
cmake -S . -B build -A x64 -DCMAKE_PREFIX_PATH="C:/SDK/NativeWinUI"
cmake --build build --config Release
```

DLL 方式还需把 SDK 的 `bin/NativeWinUI.dll` 放到应用 EXE 同目录。应用窗口和消息循环由宿主工程提供。发布附件不包含框架实现源码、测试源码或示例源码，仅保留接入必需的公开头文件。

## 🔢 版本规则

首版为 **0.1.0**，之后只递增最后一位：`0.1.1` → `0.1.2` → ……；Git 标签使用 `v0.1.N`。公开版本不覆盖旧附件，SDK、Gallery 文件版本和 Release 使用同一版本号。版本号、校验值和构建信息可在每次 Release 的清单中查看。

维护者在源码仓库运行 `powershell -File tools/release.ps1 -Publish`，即可自动计算下一版本、构建、打包、验证并发布到本仓库。只运行 `tools/release.ps1` 则仅在本地准备候选产物。

## 📄 许可证

本仓库采用 [MIT 许可证](LICENSE)。分发的第三方代码及资源遵循各自许可证，完整说明随 SDK 的 `licenses/` 一并提供。
