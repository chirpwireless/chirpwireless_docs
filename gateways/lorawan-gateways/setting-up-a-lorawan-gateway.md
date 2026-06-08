---
description: Register your home gateway in Chirp, download its security certificate, and get it online in minutes.
---

# Setting Up Your Gateway

Getting your gateway connected to Chirp takes just a few minutes. You'll register it in the app, download a security certificate, and then configure the gateway hardware to talk to Chirp.

## What you'll need

- Your gateway hardware, plugged in and connected to your home internet (Ethernet or Wi-Fi, depending on the model)
- The **Gateway EUI** — a 16-character code printed on a sticker on the gateway itself or on its packaging. It looks something like `A8:40:41:FF:FE:12:34:56`.

## Register your gateway in Chirp

1. Click **Gateways** in the sidebar.
2. Click **Add gateway**.
3. Enter a **Name** for your gateway — something that helps you remember where it is. For example, "Living Room Gateway" or "Garage Hub."
4. Select your **Region** from the dropdown. This needs to match the frequency your gateway was built for. If you bought it for use in your country, the right option is usually clear:

   | If you're in... | Select |
   |---|---|
   | Europe | EU868 |
   | United States | US915-0 or US915-1 |
   | Australia | AU915-0 |
   | Asia-Pacific | AS923 or AS923-2 |
   | India | IN865 |
   | South Korea | KR920 |

   Not sure? Check the label or spec sheet that came with your gateway — it will mention the frequency band.

5. Enter your **Gateway EUI** — the 16-character identifier from the gateway label.
6. Click **Next**.

## Download your security certificate

After registering, Chirp shows a confirmation screen with:

- Your gateway's **Name**, **Region**, and **Gateway EUI** for you to double-check.
- An **LNS Address** — click the copy icon to save this to your clipboard. You'll need it in a moment.
- A **certs.zip** file — click the download icon to save this certificate bundle to your computer.

Click **Continue** to finish registration in Chirp. You'll see a message confirming your gateway was added successfully.

## Configure your gateway hardware

Now you need to tell your gateway where to send data:

1. Open your gateway's settings page — this is usually a web interface you access by typing the gateway's IP address into your browser. Check your gateway's quick-start guide for how to reach it.
2. Find the LoRaWAN or Basics Station settings section.
3. Paste the **LNS Address** you copied from Chirp.
4. Upload the certificates from the **certs.zip** file you downloaded.
5. Save and restart the gateway if it asks you to.

The exact screens look different for each gateway brand — your gateway's own manual will show you exactly where to paste the address and upload the certificates.

## Verify it's working

Within a few minutes, your gateway should appear as online in the **Gateways** list in Chirp. If you don't see it come online:

- Double-check that the LNS Address was pasted correctly (no extra spaces)
- Make sure the certificate files were uploaded to the right place
- Confirm your gateway is connected to the internet
- Try restarting the gateway

Once it's online, your gateway is ready to start receiving sensor data. Head to [Connections](../../connectors/) to set up the link between your gateway and Chirp's sensor management.

These steps are the current gateway setup path. Other options you might see in the app that aren't related to smart home setup can be safely skipped.

## Tips for best coverage

- **Put it up high.** A shelf, wall mount, or the top of a bookcase — higher placement means better range.
- **Central is best.** If your gateway is in the middle of your home, signals can reach every direction.
- **One is usually enough.** A single gateway can cover a typical house or apartment. LoRaWAN signals go through walls, so you don't need one per room.
- **Keep the certificates safe.** The `certs.zip` file is like a key to your gateway's connection. Don't share it. If you ever need a fresh one, you can regenerate it from your gateway's settings page.
