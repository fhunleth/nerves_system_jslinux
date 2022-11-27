# JSLinux Support

[![CircleCI](https://circleci.com/gh/fhunleth/nerves_system_jslinux.svg?style=svg)](https://circleci.com/gh/fhunleth/nerves_system_jslinux)
[![Hex version](https://img.shields.io/hexpm/v/nerves_system_jslinux.svg "Hex version")](https://hex.pm/packages/nerves_system_jslinux)

This is the base Nerves System configuration for a [JSLinux](#jslinux). This is
not a complete Nerves port since some features like firmware updates and a
persistent data partition are not implemented at all. The port is intended as a
proof of concept and a browser-only way of demoing some simple features.

![JSLinux Screenshot](assets/images/screenshot.png)

| Feature              | Description                     |
| -------------------- | ------------------------------- |
| CPU                  | 64 bit RISC-V                   |
| Memory               | 128 MB (configurable)           |
| Storage              | Temporary 			 |
| Linux kernel         | 5.19                            |
| IEx terminal         | VirtIO `ttyhvc0`                |
| GPIO, I2C, SPI       | Emulated - [Elixir Circuits](https://github.com/elixir-circuits) |
| Display              | Yes, but not supported yet      |
| ADC                  | No                              |
| PWM                  | No                              |
| UART                 | No                              |
| Camera               | No                              |
| Ethernet             | VirtIO, but not supported yet   |
| WiFi                 | No                              |
| RTC                  | No                              |
| HW Watchdog          | Software                        |

## Using

The most common way of using this Nerves System is create a project with `mix
nerves.new` and add `jslinux` references where needed and in a similar way
to the default systems like `bbb`, etc. Then export `MIX_TARGET=jslinux`.
See the [Getting started
guide](https://hexdocs.pm/nerves/getting-started.html#creating-a-new-nerves-app)
for more information.

If you need custom modifications to this system for your device, clone this
repository and update as described in [Making custom
systems](https://hexdocs.pm/nerves/customizing-systems.html).

## Example use

This example assumes some familiarity with Nerves. To use this system, you'll
need OTP 25. Follow the [Nerves installation
instructions](https://github.com/nerves-project/nerves/blob/main/docs/Installation.md)
for additional system dependencies.

Creating a new hello world application:

```sh
mix nerves.new hello_jslinux
cd hello_jslinux
```

Open up your `mix.exs` and add `:jslinux` to the `@all_targets` list at
the top. It's ok to delete targets that you don't plan on using.

Then add the `:nerves_system_jslinux` dependency to the `deps` function:

```elixir
    {:nerves_system_jslinux, "~> 0.1", runtime: false, targets: :jslinux},
```

This will load the latest released version. To use the latest code on the `main`
branch here, add the following line:

```elixir
    {:nerves_system_jslinux, runtime: false, targets: :jslinux, nerves: [compile: true], git: "https://github.com/fhunleth/nerves_system_jslinux", branch: "main"}
```

To build, run:

```sh
export MIX_TARGET=jslinux
mix deps.get
mix firmware
...
```

## Console access

The console appears in the JSTerm Window.

## Networking

The board has a VirtIO network interfaces. I haven't figured out how to use it
yet.

## Thanks

This port uses Fabrice Bellard's [TinyEMU](https://bellard.org/tinyemu/).
[Ahmad Fatoum's fork](https://github.com/a3f/TinyEMU) had a super helpful fix
for newer versions of Emscripten. This unblocked me when I got stuck trying out
various Emscripten versions to try to fix runtime errors.

