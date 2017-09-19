A tiny [Particle Photon](https://www.particle.io/) program for remote starting a PC.
The Photon board is (almost) directly wired to the motherboard headers,
perfectly replicating the actions of physically pressing your computer's power and reset buttons.

# How it works

Most standard desktop computer motherboards have a set of front panel headers exposed for various purposes.
Among these are pins used to boot and reset the system. When a motherboard is installed in a case,
wires from the power and reset buttons are plugged directly into these headers. Each button has a + and - pin,
and the act of pressing a button simply closes the circuit between them.

This project consists of a WiFi-enabled microcontroller spliced between these headers, giving the capability to remotely initiate a
[cold boot](https://en.wikipedia.org/wiki/Reboot_(computing)#Cold_vs._warm_reboot) or
[hard reboot](https://en.wikipedia.org/wiki/Reboot_(computing)#Hard_reboot).
The only requirement for it to function is that your system's PSU is switched on and plugged in.

# What you'll need

* [NPN transistor](https://learn.sparkfun.com/tutorials/transistors) (x2)

* [Particle Photon](https://store.particle.io/) (x1)

* Some wires 'n stuff

* Breadboard (x1) or decent soldering skills

# Setup
If you're unfamiliar with the Particle Photon platform,
[read their Getting Started guide](https://docs.particle.io/guide/getting-started/start/photon/).

It's highly recommended that you use an NPN transitor as a switch to protect both your motherboard and the Photon from damage.

**Disclaimer: I am not responsible for any electronics damaged while following these instructions. Use at your own risk.**

If your motherboard's front panel headers aren't labeled directly on the board, consult either the manual or Google.

* Wire the motherboard's POWER + pin to the E end of an NPN transistor. Wire the POWER - pin to C on the same NPN transitor.
Wire D7 to the base of the same NPN switch.

* Repeat the same process for the reset switch. Wire the motherboard's RESET + pin to the E end of an NPN transistor. Wire the RESET - pin to C on the same NPN transitor.
Wire D1 to the base of the same NPN switch. Note: this step is optional, and best skipped if you don't have a need for remotely hard rebooting your system.

* Wire the computer case's power and reset buttons their corresponding NPN switches,
including ground (from the button) to ground (on the motherboard), so that they remain functional.

* Flash `lamprey.cpp` to your Photon

I recommend powering the Photon using an internal USB header on the same motherboard, if possible.

# How to use

See [Particle's documentation on calling a Cloud function](https://docs.particle.io/reference/firmware/photon/#particle-function-).

Call the function `pc-power` with the argument `togglePower` to trip the power switch on your computer.
Note: different operating systems behave differently when the power button is pressed,
e.g., Windows has a "Choose what the power buttons do" option under Control Panel > Power Options.

Call the function `pc-power` with the argument `reset` to trip the reset switch on your computer.

This project can also be integrated with [Pantheon](https://github.com/Nase00/pantheon), which is especially handy when set up into a PC used as a home media center.
See [documenation on how to integrated a Particle function with Pantheon](https://github.com/Nase00/pantheon/blob/master/docs/events.md#particle-photon).
