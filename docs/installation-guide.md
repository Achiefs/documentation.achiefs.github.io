---
layout: default
title: Installation guide
nav_order: 2
---

# Installation guide
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

# Requirements

File Integrity Monitor software installation will require the following to work:
- At least 1 Core CPU.
- At least 128 MB of memory.
- At least 1 GB of storage (used storage will increase over time).

Recommended:
- 2 Core CPU.
- 1 GB of memory.
- 128 GB of storage.

Download the latest version at [Download release page](https://github.com/Achiefs/fim/releases) and select your architecture and system.

For Windows: download the `msi` and jump to [Windows install](#windows-install)

For Debian-based systems: download the `deb` and jump to [Debian-based install](#debian-based-install)

For CentOS-based systems: download the `rpm` and jump to [CentOS-based install](#centos-based-install)

---

# Supported platforms

- Supported operating systems:
  - Ubuntu Xenial or greater.
  - CentOS 7 or greater.
  - Windows Server 2016 or greater.
  - Windows 7 or greater.
  - macOS BigSur or greater.

- Supported architectures:
  - Linux
    - ARM64: [AARCH64, ARM64].
    - AMD64: [X86_64, AMD64].
  - Windows
    - X86_64.
  - macOS
    - x86_64 (Intel).
    - ARM64 (Apple Silicon).

---

# Debian-based install

Debian-based systems will require a specific package extension and instructions. FIM is designed to install and work with the provided `deb` extension package. You can install FIM in Debian systems with the following required steps:

1. Download the Debian package from [Releases page](https://github.com/Achiefs/fim/releases) 
2. Run from a terminal `dpkg -i fim*.deb` to install the package.
3. Start FIM software with `systemctl start fim`.

From this point, FIM will start to work with the default configuration. It will report each event detected to a local JSON file. The location of the file is `/var/lib/fim/events.json`.

If you detect some problem in FIM performance, you could retrieve the process log from `/var/log/fim/fim.log`.

{: .note}
> Available commands in systemctl [start, stop, restart, status].

{: .note}
> If you wish to tune up FIM, take a look at [Configuration file]({% link docs/configuration-file.md %})

---

# CentOS-based install

CentOS-based systems will require a specific package extension and instructions. FIM is designed to install and work with the provided `rpm` extension package. You can install FIM in CentOS systems with the following required steps:

1. Download the CentOS package from [Releases page](https://github.com/Achiefs/fim/releases) 
2. Run from a terminal `yum install fim-*.rpm` to install the package.
3. Start FIM software with `systemctl start fim`.

From this point, FIM will start to work with the default configuration. It will report each event detected to a local JSON file. The location of the file is `/var/lib/fim/events.json`.

If you detect some problem in FIM performance, you could retrieve the process log from `/var/log/fim/fim.log`.

{: .note}
> Available commands in systemctl [start, stop, restart, status].

{: .note}
> If you wish to tune up FIM, take a look at [Configuration file]({% link docs/configuration-file.md %})

---

# Windows install

Windows systems will require a specific package extension and instructions. FIM is designed to install and work with the provided `msi` extension package. You can install FIM in Windows systems with the following required steps:

1. Download the Windows package from [Releases page](https://github.com/Achiefs/fim/releases) 

*From Powershell terminal*
1. `.\fim-VERSION-1-x64.msi /q` (Replace `VERSION` with the downloaded version, e.g. `0.4.5`).
2. Start File monitor service with `NET START FimService`.

*From user interface* (MSI double click)
The installer will guide you through graphical installation. Follow the interface steps to install FIM.

From this point, FIM will start to work with the default configuration. It will report each event detected to a local JSON file. The location of the file is `C:\ProgramData\fim\events.json`.

If you detect some problem in FIM performance, you could retrieve the process log from `C:\ProgramData\fim\fim.log`.

{: .note}
> Available commands [START, STOP].

{: .note}
> If you wish to tune up FIM, take a look at [Configuration file]({% link docs/configuration-file.md %})

---

# macOS install

macOS systems will require a specific package extension and instructions. FIM is designed to install and work with the provided `pkg` extension package. You can install FIM in macOS systems with the following steps:

*From terminal*
1. Download the macOS package from [Releases page](https://github.com/Achiefs/fim/releases) 
2. Run from a terminal `sudo installer -pkg fim*.pkg -target /` to install the package.
3. Start FIM software with `sudo launchctl load -w /Library/LaunchDaemons/com.Achiefs.fim.launchd.plist`.

*From user interface* (PKG double click)
The installer will guide you through graphical installation. Follow the interface steps to install FIM.

From this point, FIM will start to work with the default configuration. It will report each event detected to a local JSON file. The location of the file is `/var/lib/fim/events.json`.

If you detect some problem in FIM performance, you could retrieve the process log from `/var/log/fim/fim.log`.

{: .note}
> Available commands in launchd [load, unload].

{: .note}
> If you wish to tune up FIM, take a look at [Configuration file]({% link docs/configuration-file.md %})

---

# Testing FIM events

After starting FIM, it will produce events detected by your host. You may want to generate a testing event to check all is working right in your environment.

*Produce event in FIM Linux*
Run `touch /etc/fake_file.txt` (With default configuration) in your terminal. At the same time, review the `/var/lib/fim/events.json` file. It will store each produced event in JSON format.
Remove the file with `rm /etc/fake_file.txt`. A new event should appear.

*Produce event in FIM Windows*
Run `echo TEST > C:\Users\YOUR_USERNAME\fake_file.txt` in your terminal (Replace `YOUR_USERNAME` with the user you are running). At the same time, review the `C:\ProgramData\fim\events.json` file. It will store each produced event in JSON format.
Remove the file with `rm C:\Users\YOUR_USERNAME\fake_file.txt`. A new event should appear.

---

# SystemD usage

FIM includes a SystemD service file for easy management of FIM process status. This service file comes by default with RPM and DEB-based packages.
The allowed commands of FIM SystemD integration are the following:
- `systemctl start fim`, start FIM process.
- `systemctl stop fim`, stop the FIM process.
- `systemctl status fim` returns the current status of the FIM process and stdout trace for troubleshooting purposes.

If you installed FIM manually without a package, you could set up your service file by following the section [Development/Setting SystemD service]({% link docs/development.md %}).
