---
layout: default
title: Development
nav_order: 4
---

# Development
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

# Set up environment

To start contributing to FIM repositories, you will need the following packages and dependencies:

*Generic dependencies for Linux systems*
- Git.
- GCC.
- RustC and Cargo.
- cURL.
- TAR.
- GZIP.

*For Debian-based systems dependencies*
- devscripts
- equivs
- pkg-config
- libssl-dev

*For CentOS-based systems dependencies*
- rpm-build
- openssl-devel

*Windows systems*
- Git.
- RustC and Cargo.
- Light and Candle from MSI toolset.

---

## Installing Rust
Install Rust in the mentioned systems can be performed following the steps:

### Linux systems
1. Run `curl https://sh.rustup.rs -sSf | sh` to download and install Rust. Follow the required steps with the recommended installation.
2. Reload the terminal and try cargo with `cargo --version`.

---

### Windows systems
1. Download Rust from the official [Rust page](https://www.rust-lang.org/tools/install).
2. Double-click on the installer and follow the UI steps.
3. Reload the terminal and try cargo with `cargo --version`.

---

## Installing dependencies
You can install each system dependency with the below code block.

### Debian dependencies
```
sudo apt update
sudo apt install -y git curl gcc tar gzip devscripts equivs pkg-config libssl-dev
```

### CentOS dependencies
```
sudo yum install -y git curl gcc tar gzip rpm-build openssl-devel
```

### Windows dependencies
1. Checkout and get Git from [Git downloads page](https://git-scm.com/downloads)
2. Checkout and get WIX Toolset from [WIX page](https://wixtoolset.org/docs/wix3/)

---

# Build FIM
FIM requires a compilation or package to run or install in the host. The repository provides tools to perform both options.

## Compile and run FIM
With the dependencies installed, it will only require fetching the repository source code and building with the following steps:
1. Fetch the Git repository with `git clone https://github.com/Achiefs/fim.git`.
2. Go to the repository `cd fim`.
3. Compile FIM `cargo build --release`.
4. Run FIM with `cargo run` (Unix systems).
5. Run FIM with `cargo run -- -f` to run FIM in the foreground (Windows systems only)

{: .note}
> FIM executable is stored at the `target/release` or `target/debug` folder, depending on cargo build performed `--release` or not.

---

## Build FIM packages
Custom FIM packages are proper to deploy FIM-customized features in specific environments.
It is recommended to use Docker. It will maintain your environment clean and secure.

Build FIM package is automated. Follow the below steps to produce the FIM package:
1. Run a new docker of the desired package, e.g. `docker run -it --rm ubuntu:xenial`.
2. Install [required dependencies](#installing-dependencies) inside the container.
3. Clone the FIM repository and go to package folder `pkg/deb`.
4. Run the `./builder.sh` script to perform build and package generation.
5. Retrieve the package produced in the current folder. This package has a `.deb` extension.

{: .note}
> Perform the same steps to build `rpm` or `msi` packages. It is required to use ARM hardware to build ARM packages.