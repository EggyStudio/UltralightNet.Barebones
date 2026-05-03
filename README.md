![header.png](https://raw.githubusercontent.com/EggyStudio/UltralightNet.Bundle/refs/heads/main/.github/assets/header.png)

# UltralightNet.Bundle

[![GitHub Packages](https://img.shields.io/badge/GitHub%20Packages-UltralightNet.Bundle-2dba4e?logo=github)](https://github.com/EggyStudio/UltralightNet.Bundle/packages)
[![publish-package](https://github.com/EggyStudio/UltralightNet.Bundle/actions/workflows/publish-package.yml/badge.svg?branch=main)](https://github.com/EggyStudio/UltralightNet.Bundle/actions/workflows/publish-package.yml)
[![Release](https://img.shields.io/github/v/release/EggyStudio/UltralightNet.Bundle?include_prereleases&sort=semver&logo=github&label=Release)](https://github.com/EggyStudio/UltralightNet.Bundle/releases)
[![License: MPL-2.0](https://img.shields.io/badge/License-MPL--2.0-brightgreen.svg)](LICENSE)
[![.NET 10](https://img.shields.io/badge/.NET-10.0-512BD4?logo=dotnet)](https://dotnet.microsoft.com/)
[![Platform](https://img.shields.io/badge/platform-win--x64%20%7C%20linux--x64%20%7C%20osx--x64%20%7C%20osx--arm64-informational)](#supported-runtimes)
[![Stars](https://img.shields.io/github/stars/EggyStudio/UltralightNet.Bundle?style=social)](https://github.com/EggyStudio/UltralightNet.Bundle/stargazers)

A single-package .NET binding for the [Ultralight](https://ultralig.ht/) HTML rendering engine.

This package bundles everything needed to embed Ultralight in a .NET application:

- `UltralightNet` - managed bindings for the Ultralight C API
- `UltralightNet.AppCore` - managed bindings for AppCore (windowing, font loader, file system, default logger)
- Native binaries for `win-x64`, `linux-x64`, `osx-x64`, and `osx-arm64` (Ultralight, UltralightCore, WebCore, AppCore)

It targets **.NET 10**.

## Install

```sh
dotnet add package UltralightNet.Bundle
```

## Quick start

```csharp
using UltralightNet;
using UltralightNet.AppCore;

AppCoreMethods.SetPlatformFontLoader();
AppCoreMethods.ulEnablePlatformFileSystem("./assets");
AppCoreMethods.ulEnableDefaultLogger("./ultralight.log");

using var renderer = ULPlatform.CreateRenderer(new ULConfig());
using var view = renderer.CreateView(1280, 720, new ULViewConfig());

view.URL = "https://example.com";

while (!view.IsLoading)
{
    renderer.Update();
    renderer.Render();
}
```

The native binaries are deployed automatically into `runtimes/<rid>/native/` when your project builds.

## Supported runtimes

| RID         | Libraries |
|-------------|-----------|
| `win-x64`   | `Ultralight.dll`, `UltralightCore.dll`, `WebCore.dll`, `AppCore.dll` |
| `linux-x64` | `libUltralight.so`, `libUltralightCore.so`, `libWebCore.so`, `libAppCore.so` |
| `osx-x64`   | `libUltralight.dylib`, `libUltralightCore.dylib`, `libWebCore.dylib`, `libAppCore.dylib` |
| `osx-arm64` | `libUltralight.dylib`, `libUltralightCore.dylib`, `libWebCore.dylib`, `libAppCore.dylib` |

## Build & pack locally

```sh
dotnet pack -c Release
```

Output: `bin/Release/UltralightNet.Bundle.<version>.nupkg` (and `.snupkg`).

## License

Source code in this repository is licensed under [MPL-2.0](LICENSE).

The bundled Ultralight native binaries are redistributed under the
[Ultralight Free License](https://ultralig.ht/) - review their terms before
shipping a commercial product.

