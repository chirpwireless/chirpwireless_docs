---
description: Set up a Raspberry Pi for Chirp Hub. Put Ubuntu on the microSD card, run one setup script, then install Chirp Hub.
---

# How Do I Set Up a Raspberry Pi for Chirp Hub?

Setting up the Pi takes three steps. First you put Ubuntu, the operating system, on the microSD card. Then you run one setup script that installs everything the hub needs. Finally you install the Chirp Hub app. Plan on 30 to 45 minutes, and most of that is waiting for downloads.

You follow the same steps whether or not your Pi has a LoRaWAN card. The setup script checks for the card by itself and only sets up the gateway when it finds one.

## How do I write Ubuntu to the microSD card?

The Raspberry Pi setup for Chirp Hub needs **Ubuntu Server 24.04 LTS or 26.04 LTS (64-bit)**.

1. Download **Raspberry Pi Imager** from [raspberrypi.com/software](https://www.raspberrypi.com/software/) to your computer, and insert the microSD card into your card reader.
2. In Raspberry Pi Imager, choose:
   * **Device:** your Pi, a Raspberry Pi 4 or a Raspberry Pi 5.
   * **Operating system:** **Other general-purpose OS → Ubuntu → Ubuntu Server 24.04 LTS (64-bit)**. If Imager offers 26.04 LTS, that works too.
   * **Storage:** the microSD card.
3. When Imager asks whether you want to customize the settings, say yes, and then:
   * choose a **hostname**, for example `chirp-hub`;
   * choose a **username and password**. You'll use them to sign in to the Pi, and Chirp Hub asks for this password whenever it changes something on the system;
   * add your home **Wi-Fi** if the Pi won't be on a network cable;
   * set your **time zone and keyboard layout**;
   * under **Services**, turn on **SSH** if you'd like to finish the setup from your own computer. SSH lets you type commands on the Pi from another computer's terminal, so you don't need the Pi's own keyboard.
4. Write the card. Now put it in the Pi, attach the network cable, a screen, a keyboard and a mouse, and connect the power supply last. The Pi starts as soon as it gets power.

The first time it starts, Ubuntu takes a few minutes to finish setting itself up. After that, log in with the username and password you chose. You can do it on the Pi's screen, or from your own computer with `ssh <username>@chirp-hub.local`.

Ubuntu Server has no desktop yet, so after logging in you're at a text prompt: a line where you type commands. That's where the next steps happen.

## How do I run the Raspberry Pi setup script? {#how-do-i-get-the-pi-ready-for-the-lorawan-card-and-radios}

At the prompt, type these three commands to download the setup script and run it:

```sh
git clone https://github.com/chirpdepin/raspberry-pi-iot-hub.git
cd raspberry-pi-iot-hub
sudo ./scripts/install-ubuntu.sh --with-desktop
```

That's the only command you need, with or without a LoRaWAN card. It runs for 10 to 20 minutes. While it runs, it:

* updates Ubuntu;
* installs Docker, which Chirp Hub uses to run your camera recorders;
* installs what the Zigbee and Thread radio sticks need, and keeps track of each stick by its serial number;
* looks for a LoRaWAN card, and if it finds one, reads the card's gateway ID and installs the gateway software;
* because of `--with-desktop`, adds a simple screen session that opens Chirp Hub when the Pi starts, plus the Firefox web browser and a tool for opening zip files.

When it's done, the script tells you what it set up.

**If your Pi has a LoRaWAN card**, the script prints a line starting with **Concentrator**, followed by the gateway ID. It also tells you the gateway is installed but not registered yet. That's expected: you register it later from Chirp Hub.

**If your Pi has no LoRaWAN card**, the script ends by telling you two things: the Pi is ready for cameras, Zigbee and Thread, and it isn't a LoRaWAN gateway because there's no card. Everything else is installed and works. If you add a card later, run the same command again and it sets up the gateway.

Sometimes the script ends with **a reboot is required**. Restart with `sudo reboot`, log back in, and start `sudo ./scripts/install-ubuntu.sh --with-desktop` a second time. That often happens on the first run: Ubuntu's updates, or the connection the LoRaWAN card uses, only take effect after a restart. Running the script again is always safe: it skips everything that's already done.

Card fitted, restarted, and still no card found? Go to [the troubleshooting steps](troubleshooting.md#what-if-the-setup-script-says-the-concentrator-did-not-answer).

## How do I install Chirp Hub on the Raspberry Pi?

Still at the same prompt, these commands fetch the newest Chirp Hub package for the Pi and install it:

```sh
curl -s https://api.github.com/repos/chirpdepin/raspberry-pi-iot-hub/releases \
  | grep -o 'https://[^"]*chirp-hub_[^"]*_arm64\.deb' | head -1 | xargs wget
sudo apt install ./chirp-hub_*_arm64.deb
```

The first command finds the newest `chirp-hub_<version>_arm64.deb` among the project's releases and downloads it. If you prefer, you can download that file in a browser from the [Chirp Hub release page](https://github.com/chirpdepin/raspberry-pi-iot-hub/releases/tag/chirp-v0.1.1) and copy it to the Pi.

Then restart the Pi:

```sh
sudo reboot
```

Don't skip this restart. The setup script gave your user account access to the radio sticks and the Zigbee settings, and that access only takes effect after a restart. Without it, Chirp Hub can't reach them.

## What should I see after the restart?

With a screen attached, you don't need to log in: the Pi does that for you, and **Chirp Hub** fills the screen, starting on the **Dashboard**:

* **This device** shows the Raspberry Pi, its memory, its processors and Docker.
* The **LoRaWAN Gateway** card says **LoRaWAN radio found. It is not set up yet.** if your Pi has the card. Without a card, it says there's no LoRaWAN radio, which is expected.
* The **Zigbee** card shows your Zigbee stick, if you've plugged one in.
* The **Cameras** card says **No cameras yet**.

<figure><img src="../../.gitbook/assets/chirp-hub-dashboard.jpg" alt="Chirp Hub Dashboard with the device details and one card each for cameras, LoRaWAN, Zigbee and Thread"><figcaption><p>Your device on the left, and a card for each part of your setup on the right.</p></figcaption></figure>

You use Chirp Hub on the Pi's own screen. Whenever you want to add a camera or a device later, plug a screen and keyboard back in. You can unplug them in between: the hub keeps recording your cameras, running Zigbee and, if you set one up, working as a gateway.

## What do I set up next?

Set up what you want, in any order:

1. **LoRaWAN gateway**, only if your Pi has the card. You register it in Chirp and add its certificates: [How Do I Use a Raspberry Pi as a LoRaWAN Gateway?](lorawan-gateway.md)
2. **Cameras**: find and add your home cameras: [How Do I Connect Home IP Cameras to Chirp Hub?](../cameras.md). On your first camera you might get **Docker is installed, but this account is not allowed to use it yet.** Select **Fix permissions** and type your password, and it carries on.
3. **Zigbee**: start the network and pair your devices: [How Do I Pair Zigbee Devices with Chirp Hub?](../zigbee.md)
4. **Thread**: give your Thread radio its job: [How Do I Add Thread to Chirp Hub?](../thread.md)

## What else should I know about Chirp Hub on a Raspberry Pi?

* Whenever Chirp Hub changes something on the system, such as starting the gateway, installing certificates or starting Zigbee for the first time, it asks for your password. That's the Pi password you chose in Raspberry Pi Imager.
* Updating works like installing: get the newer `.deb` and install it on top of the current one. Your gateway certificates, your Zigbee network and your cameras stay as they are.

Next: [How Do I Use a Raspberry Pi as a LoRaWAN Gateway?](lorawan-gateway.md) No LoRaWAN card? Go to [How Do I Connect Home IP Cameras to Chirp Hub?](../cameras.md)
