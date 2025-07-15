# Zed

[![CI](https://github.com/zed-industries/zed/actions/workflows/ci.yml/badge.svg)](https://github.com/zed-industries/zed/actions/workflows/ci.yml)

Welcome to Zed, a high-performance, multiplayer code editor from the creators of [Atom](https://github.com/atom/atom) and [Tree-sitter](https://github.com/tree-sitter/tree-sitter).

---

### Installation

On macOS and Linux you can [download Zed directly](https://zed.dev/download) or [install Zed via your local package manager](https://zed.dev/docs/linux#installing-via-a-package-manager).

Other platforms are not yet available:

- Windows ([tracking issue](https://github.com/zed-industries/zed/issues/5394))
- Web ([tracking issue](https://github.com/zed-industries/zed/issues/5396))

### Developing Zed

- [Building Zed for macOS](./docs/src/development/macos.md)
- [Building Zed for Linux](./docs/src/development/linux.md)
- [Running Collaboration Locally](./docs/src/development/local-collaboration.md)

- [**Building Zed for Windows**](./docs/src/development/windows.md)

using this page, can you simplify all of this into perhaps a vscode tasks.json keeping in mind im running windows 11 , vscode, and powershell...but thi entire page needs to be simlified and an easier build path must be created.:
https://zed.dev/docs/development/windows..what d  you mean provide the build steps everything is on this page that is specifically related to the zed build for the windows version.......use the most like to succeed and always Production over dev environments...

https://zed.dev/docs/development/windows
https://github.com/hannahbellesheart/ide-rust-zed/

here is the config.toml

```toml
[build]
# v0 mangling scheme provides more detailed backtraces around closures
rustflags = ["-C", "symbol-mangling-version=v0", "--cfg", "tokio_unstable"]

[alias]
xtask = "run --package xtask --"

[target.x86_64-unknown-linux-gnu]
linker = "clang"
rustflags = ["-C", "link-arg=-fuse-ld=mold"]

[target.aarch64-unknown-linux-gnu]
linker = "clang"
rustflags = ["-C", "link-arg=-fuse-ld=mold"]

[target.'cfg(target_os = "windows")']
rustflags = [
    "--cfg",
    "windows_slim_errors",        # This cfg will reduce the size of `windows::core::Error` from 16 bytes to 4 bytes
    "-C",
    "target-feature=+crt-static", # This fixes the linking issue when compiling livekit on Windows
    "-C",
    "link-arg=-fuse-ld=lld",
]

[env]
MACOSX_DEPLOYMENT_TARGET = "10.15.7"
```



### Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for ways you can contribute to Zed.

Also... we're hiring! Check out our [jobs](https://zed.dev/jobs) page for open roles.

### Licensing

License information for third party dependencies must be correctly provided for CI to pass.

We use [`cargo-about`](https://github.com/EmbarkStudios/cargo-about) to automatically comply with open source licenses. If CI is failing, check the following:

- Is it showing a `no license specified` error for a crate you've created? If so, add `publish = false` under `[package]` in your crate's Cargo.toml.
- Is the error `failed to satisfy license requirements` for a dependency? If so, first determine what license the project has and whether this system is sufficient to comply with this license's requirements. If you're unsure, ask a lawyer. Once you've verified that this system is acceptable add the license's SPDX identifier to the `accepted` array in `script/licenses/zed-licenses.toml`.
- Is `cargo-about` unable to find the license for a dependency? If so, add a clarification field at the end of `script/licenses/zed-licenses.toml`, as specified in the [cargo-about book](https://embarkstudios.github.io/cargo-about/cli/generate/config.html#crate-configuration).
