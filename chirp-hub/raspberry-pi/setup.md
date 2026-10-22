---
description: Prepare a Raspberry Pi for Chirp Hub. Write Ubuntu to the microSD card, run the setup script, then install Chirp Hub.
---

# How Do I Set Up a Raspberry Pi for Chirp Hub?

Getting the Pi ready is three steps: put Ubuntu on the microSD card, run a single setup script that readies the LoRaWAN card and the radios, and install the Chirp Hub app. Expect 30–45 minutes, mostly spent waiting for downloads.

## How do I write Ubuntu to the microSD card?

The Raspberry Pi setup for Chirp Hub needs **Ubuntu Server 24.04 LTS or 26.04 LTS (64-bit)**.

1. Download **Raspberry Pi Imager** from [raspberrypi.com/software](https://www.raspberrypi.com/software/) onto your computer, and slot the microSD card into the card reader.
2. In Raspberry Pi Imager, pick:
   * **Device:** the Pi you have, a Raspberry Pi 4 or a Raspberry Pi 5.
   * **Operating system:** **Other general-purpose OS → Ubuntu → Ubuntu Server 24.04 LTS (64-bit)**, or pick 26.04 LTS when Imager lists it.
   * **Storage:** the microSD card.
3. When Imager asks whether you want to customize the settings, say yes and:
   * pick a **hostname**, for example `chirp-hub`;
   * choose a **username and password**, which you'll use to sign in and to approve changes later on;
   * add your home **Wi-Fi** if the Pi won't be on a network cable;
   * set your **time zone and keyboard layout**;
   * under **Services**, switch on **SSH** if you'd like to finish setting up from your own computer.
4. Write the card, put it into the Pi, connect the network cable, screen and keyboard, then plug in the power.

On its first start, Ubuntu needs a few minutes to finish setting itself up. Then sign in with the username and password you picked, either on the Pi's own screen or from your computer with `ssh <username>@chirp-hub.local`.

## How do I get the Pi ready for the LoRaWAN card and radios?

Open a terminal on the Pi, fetch the hub's setup script and run it:

```sh
git clone https://github.com/chirpdepin/raspberry-pi-iot-hub.git
cd raspberry-pi-iot-hub
sudo ./scripts/install-ubuntu.sh --with-desktop
```

The script runs for 10–20 minutes. Along the way it:

* brings Ubuntu up to date;
* switches on the interface the concentrator card uses and makes sure the card **answers**, which is where a card that isn't seated properly gets spotted;
* reads the gateway ID off the card;
* installs Docker plus the LoRaWAN gateway software, which then waits for its certificates;
* installs support for the Zigbee and Thread radios, tracking each USB radio by its serial number;
* with `--with-desktop`, adds a minimal screen session that opens Chirp Hub automatically.

At the end it prints the **Concentrator**, which is the gateway ID, and tells you the gateway is installed but not registered yet. That's normal: you register it from Chirp Hub.

If the script tells you **a reboot is required**, run `sudo reboot`, sign back in and run `sudo ./scripts/install-ubuntu.sh --with-desktop` again. It's safe to run more than once, since it skips anything that's already done.

If it stops with **the concentrator did not answer**, go to [Why Is My Raspberry Pi Hub Not Working?](troubleshooting.md#what-if-the-setup-script-says-the-concentrator-did-not-answer)

## How do I install Chirp Hub on the Raspberry Pi?

Still in the Pi's terminal, download the newest Chirp Hub package for the Pi and install it:

```sh
curl -s https://api.github.com/repos/chirpdepin/raspberry-pi-iot-hub/releases \
  | grep -o 'https://[^"]*chirp-hub_[^"]*_arm64\.deb' | head -1 | xargs wget
sudo apt install ./chirp-hub_*_arm64.deb
```

The first command looks through the project's releases for the newest `chirp-hub_<version>_arm64.deb` and downloads it. You can also fetch that file in a browser from the [Chirp Hub release page](https://github.com/chirpdepin/raspberry-pi-iot-hub/releases/tag/chirp-v0.1.1) and copy it over to the Pi.

Then restart the Pi:

```sh
sudo reboot
```

The restart matters for another reason too: it activates the user groups the script added, and without them Chirp Hub can't reach the radios or the Zigbee settings.

## What should I see after the restart?

With a screen plugged in, the Pi logs itself in and **Chirp Hub** fills the screen, starting on the **Dashboard**:

* **This device** lists the Raspberry Pi, its memory, processors and Docker.
* **LoRaWAN Gateway** reads **LoRaWAN radio found. It is not set up yet.**
* **Zigbee** shows the coordinator, if you've plugged one in.
* **Cameras** reads **No cameras yet.**

<figure><img src="../../.gitbook/assets/chirp-hub-dashboard.jpg" alt="Chirp Hub Dashboard with the device details and one card each for cameras, LoRaWAN, Zigbee and Thread"><figcaption><p>Your device on the left, and a card for every capability on the right.</p></figcaption></figure>

With no screen, the Pi works just the same: the gateway, Zigbee and the cameras keep running. You only need a screen while you're setting things up in Chirp Hub.

## What do I set up next?

Set up the capabilities you want, in whatever order suits you:

1. **LoRaWAN gateway** — register it in Chirp and add its certificates: [How Do I Use a Raspberry Pi as a LoRaWAN Gateway?](lorawan-gateway.md)
2. **Zigbee** — start the network and pair your devices: [How Do I Pair Zigbee Devices with Chirp Hub?](../zigbee.md)
3. **Cameras** — find and add your home's cameras: [How Do I Connect Home IP Cameras to Chirp Hub?](../cameras.md). On your first try, Chirp Hub may report **Docker is installed, but this account is not allowed to use it yet.** In that case, click **Fix permissions** and enter your password when asked.
4. **Thread** — assign your Thread radio: [How Do I Add Thread to Chirp Hub?](../thread.md)

## What else should I know about Chirp Hub on a Pi?

* Whenever Chirp Hub changes something on the system, such as starting the gateway, installing certificates or starting Zigbee for the first time, it asks for your password. That's the Pi password you set in Raspberry Pi Imager.
* To update, download the newer `.deb` and install it over the current one, the same way you installed it. Your gateway certificates, Zigbee network and cameras are kept.
