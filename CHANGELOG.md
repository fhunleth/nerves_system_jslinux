# Changelog

This project does NOT follow semantic versioning. The version increases as
follows:

1. Major version updates are breaking updates to the build infrastructure.
   These should be very rare.
2. Minor version updates are made for every major Buildroot release. This
   may also include Erlang/OTP and Linux kernel updates. These are made four
   times a year shortly after the Buildroot releases.
3. Patch version updates are made for Buildroot minor releases, Erlang/OTP
   releases, and Linux kernel updates. They're also made to fix bugs and add
   features to the build infrastructure.

## v0.3.1

* Changes
  * Fix regression when building on x86_64 Linux where wrong toolchain was used.
  * Reduce first-time Linux kernel download by using tarball source

* Updated dependencies
  * [nerves_system_br v1.21.2](https://github.com/nerves-project/nerves_system_br/releases/tag/v1.21.2)
  * [Erlang/OTP 25.1.2](https://erlang.org/download/OTP-25.1.2.README)

## v0.3.0

* Changes
  * Support aarch64 Linux builds

* Updated dependencies
  * [nerves_system_br v1.21.1](https://github.com/nerves-project/nerves_system_br/releases/tag/v1.21.1)
    and also see [nerves_system_br v1.21.0](https://github.com/nerves-project/nerves_system_br/releases/tag/v1.21.0)
  * [Buildroot 2022.08.1](http://lists.busybox.net/pipermail/buildroot/2022-October/652816.html)
  * [Erlang/OTP 25.1.1](https://erlang.org/download/OTP-25.1.1.README)

## v0.2.5

* Updated dependencies
  * [nerves_system_br v1.20.6](https://github.com/nerves-project/nerves_system_br/releases/tag/v1.20.6)
  * [Erlang/OTP 25.0.4](https://erlang.org/download/OTP-25.0.4.README)
  * [Buildroot 2022.05.2](http://lists.busybox.net/pipermail/buildroot/2022-August/650546.html)
  * Also see [Buildroot 2022.05.1 changes](http://lists.busybox.net/pipermail/buildroot/2022-July/647814.html)

## v0.2.4

* Fixes
  * Fix USB gadget mode on MacOS

## v0.2.3

This release synchronizes the device tree configuration with upstream's new
MangoPi MQ Pro device tree. This has at least two noticable changes:

1. The Blue LED is now called `":status"`. It was `"blue:indicator"` so any
   references will need to be updated.
2. The SPI device that's on the GPIO header pins is now `spidev0`. This makes it
   the same as the Raspberry Pi, so this was a welcome change.

* Updates
  * Update Linux to smauel's wip-all branch. This is currently his latest and it
    includes device tree updates specifically for the MangoPi MQ Pro.
  * Serial numbers are now 8 hex digits since collisions were found with just 4.
  * USB Gadget mode works on the OTG port (right-most port)
  * Reverting firmware works now

## v0.2.2

* Updates
  * Various deletions to the device tree to free up GPIOs that weren't used.
  * Fix I2C0 pins

* Updated dependencies
  * [nerves_system_br v1.20.4](https://github.com/nerves-project/nerves_system_br/releases/tag/v1.20.4)
  * [Erlang/OTP 25.0.3](https://erlang.org/download/OTP-25.0.3.README)

## v0.2.1

This release has several updates, but mostly makes it possible to use SPI now.

* Updates
  * Linux 5.19-rc0 (smauel's wip-d1 Linux branch)
  * SPI1 works now through the GPIO header
  * Clean up DTB handling. The U-Boot device tree is the only one that's used so
    all patching and building of the Linux one has been removed. Also U-Boot is
    updated on firmware updates. This isn't good, but it's easier than reburning
    the MicroSD card every time.

## v0.2.0

This release updates the Linux kernel to 5.18 in the hopes of fixing some Linux
kernel flakiness.

U-Boot has changed enough that I don't believe that a v0.1.1 image is
upgradable. Please rewrite your MicroSD image.

* Updates
  * Linux 5.18-rc4 (smauel's wip-d1 Linux branch)
  * Switch to the Nezha device tree since upstream updates have fixed the
    warnings that caused me to create a custom dts.
  * Enable earlycon for earlier logging from Linux

## v0.1.1

The release fixes some issues that made v0.1.0 hard to use. The flaky MMC boot
issue is still present. If your board hits it, unplugging and replugging in the
MicroSD card has been found to be a more reliable workaround than rebooting.

* Updates
  * Enable the RISC-V vector extension

* Fixes
  * Fix compilation warnings when using C standard headers. If a library had
    `-Werror`, these would end up breaking Elixir libraries that had C/C++ code.
  * Make sure that the watchdog is active during boot and can't be disabled.
    This recovers (with a reboot) from some more hangs.

## v0.1.0

This is the initial release.
