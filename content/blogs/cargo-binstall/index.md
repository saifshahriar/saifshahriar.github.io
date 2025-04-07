+++
title = "Install Rust Binaries without Compiling (ft. cargo-binstall)"
author = "Saif Shahriar"
date = "2025-04-07"
toc = true
tocBorder = true
categories = ["software"]
tags = ["rust", "software"]
+++

## Issue

Recognize this?

<!-- prettier-ignore-start -->
{{<
  img
  src="./imgs/cargo-build.png"
  link="./imgs/cargo-build.png"
  style="float: left;"
  alt="running cargo build"
>}}
<!-- prettier-ignore-end -->

Yes... Yes... The unending process of `cargo build` when you want to install a
Rust binary. It can be quite annoying as well as it feels like your computer is
having a seizure. You are just trying to install a simple tool like `ripgrep` or
`fd` and it takes ages to compile. Well, they are available as binaries. Why not
just fetch the binary instead of compiling it?

## Possible Solutions

You could manually download the binary from the GitHub releases page. But that
is a hassle. You have to find the right version, download it, also maintain it
and update it manually. This is not a good solution.

## Meet `cargo-binstall`

[`cargo-binstall`](https://github.com/cargo-bins/cargo-binstall) is a tool that
allows you to install Rust binaries without the need to compile them from
source. It fetches precompiled binaries (if available) from the `crates.io`
registry and installs them directly to your system. This leaves you with a much
faster installation process and saves you from the hassle of waiting for the
compilation to finish.

<!-- prettier-ignore-start -->
{{<
    img
    src="./imgs/cargo-binstall.png"
    link="./imgs/cargo-binstall.png"
    style="float: left;"
    alt="cargo-binstall in action"
    mouse="cargo-binstall in action"
    caption="cargo-binstall in action"
>}}
<!-- prettier-ignore-end -->

That only took 13.5 seconds to install `bat`! And all that time took just to
fetch the binary. Depending on your internet speed, it would obviously be faster
since my internet speed sucks.

All you just have to do is put the correct name for the binary you want to have
installed. For example, to install `bat`, you can run:

```bash
cargo binstall bat
```

## Bonus `cargo-install-update`

Another nifty tool that I like to use along with `cargo-binstall` is
`cargo-install-update`. It allows you to update all the installed Rust binaries
without you manually checking for updates and selecting packages to.

### Usage:

1. **Update a specific binary**: Suppose you want to update `bat`:

   ```bash
   cargo install-update bat
   ```

2. **Update all installed binaries**: Now that you have installed a lot of Rust
   binaries, updating them one by one can be a hassle. You can update all of
   them by:

   ```bash
   cargo install-update -a
   ```

3. **Check for outdated binaries**: That's all well and good, but maybe you want
   to check for outdated binaries and not install them just now. Just do:
   running:
   ```bash
   cargo install-update -l
   ```

<!-- prettier-ignore-start -->
  {{<
      img
      src="./imgs/cargo-install-update.png"
      link="./imgs/cargo-install-update.png"
      alt="cargo-install-update in action"
      mouse="listing binaries"
      caption="listing binaries with cargo-install-update"
  >}}
<!-- prettier-ignore-end -->

Looks like I need to update `cargo-binstall`. BTW, realised you can also list
all the installed binaries in this manner?

## Links:

- `cargo-binstall`: https://github.com/cargo-bins/cargo-binstall
- `cargo-install-update`: https://github.com/nabijaczleweli/cargo-update
