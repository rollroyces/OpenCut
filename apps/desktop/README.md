# OpenCut Desktop

Built with [GPUI](https://www.gpui.rs).

> [!WARNING]
> Very early. Right now this is just a window that opens.

## Running

Rust is pinned in `.prototools` at the repo root (`proto use` installs it).

```sh
moon run desktop:dev     # cargo run
moon run desktop:check   # cargo check
moon run desktop:build   # cargo build --release
```

The first build compiles GPUI from source and takes a while. The root `Cargo.lock` is committed.

## Platform requirements

- **macOS**: Xcode command line tools (Metal renderer).
- **Windows**: the MSVC linker is required to compile the Rust crates, so install
  [Visual Studio Build Tools](https://visualstudio.microsoft.com/downloads/) with the
  "Desktop development with C++" workload — e.g. from PowerShell:

  ```powershell
  winget install --id Microsoft.VisualStudio.2022.BuildTools --override "--quiet --wait --add Microsoft.VisualStudio.Workload.VCTools --includeRecommended"
  ```

  Without it the build fails with ``error: linker `link.exe` not found``. No other
  dependencies are needed (Win32 + DirectWrite).
- **Linux**: renders via Vulkan (Blade), windows via Wayland or X11 (both enabled by default). System packages (Debian/Ubuntu names): `libvulkan1` + working Vulkan drivers, `libwayland-dev`, `libx11-xcb-dev`, `libxkbcommon-x11-dev`, `libfontconfig-dev`, plus a C toolchain and `cmake`.
- **WSL2/WSLg**: uses XWayland automatically when available. GPUI 0.2.2 requires `xdg_wm_base` v2–5, while WSLg advertises v1.
