---
tags:
  - linux
  - unix
title: Suspend
description: Different ways of suspending a system
created: 2026-07-19
published:
author:
source: https://wiki.archlinux.org/title/Power_management/Suspend_and_hibernate
---
There are [multiple methods](https://docs.kernel.org/admin-guide/pm/sleep-states.html) of suspending available, notably:
## Suspend to idle

Called [S0ix](https://www.intel.com/content/www/us/en/docs/vtune-profiler/user-guide/2023-0/s0ix-states.html) by Intel, [Modern Standby](https://docs.microsoft.com/en-us/windows-hardware/design/device-experiences/modern-standby) (previously "Connected Standby") by Microsoft and [S2Idle](https://docs.kernel.org/admin-guide/pm/sleep-states.html#suspend-to-idle) by the kernel. Designed to be used instead of the **S3** [sleeping state](https://en.wikipedia.org/wiki/ACPI#Global_states "wikipedia:ACPI") for supported systems, by providing identical energy savings but a drastically reduced wake-up time.

**Tip** While this state is subject to battery drain issues on [Windows](https://www.dell.com/support/kbdoc/en-us/000143524/the-battery-drains-quicker-than-expected-on-a-dell-notebook-with-modern-standby-mode-enabled) or [macOS](https://support.apple.com/guide/mac-help/mh40773/mac) since they support waking devices in this state for network activity, the Linux software ecosystem does not currently make use of this feature and should be unaffected.
## Suspend to RAM (aka suspend)

The **S3** sleeping state as defined by ACPI. Works by cutting off power to most parts of the machine aside from the RAM, which is required to restore the machine's state. Because of the large power savings, it is advisable for laptops to automatically enter this mode when the computer is running on batteries and the lid is closed (or the user is inactive for some time).

## Suspend to disk (aka hibernate)

The **S4** sleeping state as defined by ACPI. Saves the machine's state into [swap space](https://wiki.archlinux.org/title/Swap_space "Swap space") and completely powers off the machine. When the machine is powered on, the state is restored. Until then, there is [zero](https://en.wikipedia.org/wiki/Standby_power "wikipedia:Standby power") power consumption.

Hybrid suspend (aka hybrid sleep)

A hybrid of suspending and hibernating, sometimes called **suspend to both**. Saves the machine's state into swap space, but does not power off the machine. Instead, it invokes the default suspend. Therefore, if the battery is not depleted, the system can resume instantly. If the battery is depleted, the system can be resumed from disk, which is much slower than resuming from RAM, but the machine's state has not been lost.

The kernel provides basic functionality, and some high level interfaces provide tweaks to handle problematic hardware drivers/kernel modules (e.g. video card re-initialization).