---
description: "Find your camera brand’s RTSP address, local login requirements, and stream options to bring home camera feeds into Chirp Lens."
---

# RTSP Camera URLs

To show your camera in Lens, Twin needs the address of its video feed. This **RTSP URL** tells Twin where the camera is, how to sign in, and which picture to request. You can usually build it from a short pattern instead of searching for a completely different setup for every camera.

This camera-brand directory collects common addresses and the settings needed to adapt them. Available streams depend on your particular model and firmware. A camera that works only through its manufacturer's cloud app may not provide a local RTSP feed.

## What to replace

A typical address looks like this:

```text
rtsp://username:password@cameraip:554/stream1
```

Use your camera's local username and password in place of the first two placeholders. Replace `cameraip` with the camera's local network address. `554` is the usual RTSP port; use another number if your camera's settings specify one. The ending, such as `/stream1`, chooses a stream.

Your camera password, Twin sign-in password, and Lens connection token have different jobs. Only the camera's credentials belong in its RTSP address.

## Look up a brand

Start with [Tapo](#tapo-stream1-and-stream2), [HiLook / Hikvision](#hilook-and-hikvision-numbered-channels), or [Dahua, Reolink, and Axis](#other-common-patterns). The extended directory includes [Amcrest](#amcrest), [Avigilon](#avigilon), [Bosch](#bosch), [EZVIZ](#ezviz), [Foscam](#foscam), [Hanwha / Wisenet](#hanwha-vision-and-wisenet), [i-PRO](#i-pro), [VIGI](#tp-link-vigi), [Uniview](#uniview-and-unv), and [VIVOTEK](#vivotek).

## Tapo: stream1 and stream2

These are the addresses for the main picture and the lower-quality alternative on compatible Tapo models:

```text
rtsp://username:password@cameraip:554/stream1
rtsp://username:password@cameraip:554/stream2
```

The Tapo camera in our Lens example uses `/stream1`. Before connecting yours, open the Tapo app, select the camera, and go to **Device Settings → Advanced Settings → Camera Account**. Set up that local account and use it in the URL; your TP-Link cloud login is different.

Check RTSP support before choosing a battery camera, because many battery-powered models do not offer it. Certain dual-lens models also have `/stream6` and `/stream7` for their other lens. [TP-Link's setup instructions](https://www.tp-link.com/us/support/faq/2680/) explain the model differences.

## HiLook and Hikvision: numbered channels

Our connected HiLook camera uses this substream address pattern:

```text
rtsp://username:password@cameraip:554/Streaming/Channels/102
```

For the main stream, use:

```text
rtsp://username:password@cameraip:554/Streaming/Channels/101
```

Here, `1` identifies the camera channel, while `01` and `02` select main and substream. A standalone camera generally uses channel 1. With a recorder, channel 2 becomes `201` for main or `202` for substream. This matches [Hikvision's published stream examples](https://supportusa.hikvision.com/support/solutions/articles/17000129022-do-you-have-an-example-showing-the-format-for-getting-a-rtsp-stream-from-a-camera-). Keep the path's capitalization and use the RTSP port configured on your device.

## Other common patterns

Use these when your camera supports the corresponding manufacturer's RTSP interface. Replace the placeholders before entering the address in Twin.

| Camera family | Main or default feed | Lower-bandwidth feed |
|---|---|---|
| Dahua | `rtsp://username:password@cameraip:554/cam/realmonitor?channel=1&subtype=0` | Change `subtype=0` to `subtype=1`. |
| Reolink | `rtsp://username:password@cameraip:554/Preview_01_main` | Change `main` to `sub`. |
| Axis | `rtsp://username:password@cameraip:554/axis-media/media.amp` | Choose the camera's stream profile or video parameters. |

For Dahua, `channel=1` chooses the first channel and `subtype` chooses its stream. See [Dahua's URL examples](https://dahuawiki.com/Remote_Access/RTSP_via_VLC).

Reolink uses `01` for a standalone camera; an NVR can use another channel, such as `02`. Enable RTSP on supported devices as described in [Reolink's guide](https://support.reolink.com/articles/900000630706-Introduction-to-RTSP/).

Axis can select another video channel with a parameter such as `?camera=2`. Its [streaming instructions](https://developer.axis.com/video-streaming-and-recording/video-streaming/getting-started/) explain that endpoint.

## More brands and installed camera systems

If you already have one of these cameras at home, check its RTSP settings before replacing it. The links explain the manufacturer’s stream format; the entry does not mean that every model in the range has been tested with Lens.

### Amcrest

For an IP camera, start with `subtype=0`; an extra stream uses `1`. An Amcrest recorder can need `/h264Preview_01_main` instead.

```text
rtsp://username:password@cameraip:554/cam/realmonitor?channel=1&subtype=0
```

[Stream setup reference](https://support.amcrest.com/hc/en-us/articles/360059435271-Accessing-Amcrest-Products-Using-RTSP).

### Avigilon

Copy your camera’s **RTSP Stream URI** from **Compression and Image Rate**. The example shows a primary unicast stream.

```text
rtsp://username:password@cameraip:554/defaultPrimary?streamType=u
```

[Stream setup reference](https://www.avigilon.com/fs/documents/avigilon-camera-web-interface-user-guide-en.pdf).

### Bosch

On Bosch BVIP equipment, change `inst=1` to `inst=2` for the second encoding stream.

```text
rtsp://username:password@cameraip:554/?inst=1
```

[Stream setup reference](https://knowledge.keenfinity-group.com/video-systems/article/how-is-rtsp-usage-supported-with-bosch-vip-devices).

### EZVIZ

EZVIZ documents this for C6N, TY1, and TY2. Use the local camera password described below.

```text
rtsp://admin:cameraPassword@cameraip:554/ch1/main
```

[Stream setup reference](https://m-support.ezviz.com/faq/article/How-to-set-up-C6N-TY1-TY2-as-a-webcam).

### Foscam

A lighter picture uses `/videoSub`. Port `88` is common for Foscam; your model may use another port.

```text
rtsp://username:password@cameraip:88/videoMain
```

[Stream setup reference](https://www.foscam.com/faqs/view.html?id=81).

### Hanwha Vision and Wisenet

Replace `N` with an existing video profile number from your camera’s settings.

```text
rtsp://username:password@cameraip:554/profileN/media.smp
```

[Stream setup reference](https://support.hanwhavision.com/hc/en-001/articles/47257361792659-What-are-the-RTSP-URLs-of-Hanwha-Devices).

### i-PRO

Use `stream_2` for another configured stream. Older models can use the H.264-specific path `/Src/MediaInput/h264/stream_1`.

```text
rtsp://username:password@cameraip:554/Src/MediaInput/stream_1
```

[Stream setup reference](https://i-pro.com/products_and_solutions/en/media/documentation_file/command-interface-ipro_h265models_ver114pdf).

### TP-Link VIGI

Choose `/stream2` for the lower-quality feed; sign in with the VIGI camera account.

```text
rtsp://username:password@cameraip:554/stream1
```

[Stream setup reference](https://www.tp-link.com/id/support/faq/3718/).

### Uniview and UNV

The usual substream is `/media/video2`; some models also provide `/media/video3`.

```text
rtsp://username:password@cameraip:554/media/video1
```

[Stream setup reference](https://www.uniview.com/res/202310/26/20231026_1890310_How%20to%20Get%20a%20Uniview%20Camera%27s%20RTSP%20Stream_974039_168459_0.pdf).

### VIVOTEK

Older access names include `/live.sdp` and `/live2.sdp`. Newer cameras may use a profile address instead.

```text
rtsp://username:password@cameraip:554/live.sdp
```

[Stream setup reference](https://vivotek.zendesk.com/hc/en-001/articles/900005560446--All-cameras-Anystream-compatible-How-to-use-the-Anystream-functionality-in-VIVOTEK-cameras).

For **EZVIZ**, `cameraPassword` means the local connectivity password. On the models in the linked example, this initially corresponds to the verification code on the device label. After a password change, use the new local/video encryption password. [EZVIZ explains the shared password setting](https://m-support.ezviz.com/faq/article/How-should-I-set-the-login-password-for-local-connectivity-features-supported).

For **VIVOTEK** cameras using newer stream profiles, the address can instead be:

```text
rtsp://username:password@cameraip:554/media2/stream.sdp?profile=profileToken
```

Get `profileToken` from the camera’s video profile settings. It is a camera profile identifier, not your private Lens connection token. Firmware can also expose names of the form `/live1sN.sdp`; copy the actual access name for your chosen stream. [VIVOTEK’s newer-firmware guide](https://vivotek.zendesk.com/hc/en-001/articles/4952515434649--All-cameras-2-2002-x-x-and-later-version-How-to-get-RTSP-streaming-with-camera-firmware-version-2-2002-x-x-and-later-version) covers these differences.

## Add the address and check the picture

In Twin, open **Settings → Camera Connector** and enter the complete address in the stream URL field. If your camera supplies a substream, enter that in the separate substream field. Save the settings, then confirm that video arrives before continuing with [camera pairing](connecting-a-camera.md).

The main stream usually gives you more detail; the substream uses fewer resources. Actual resolution comes from the camera's video settings. Start with a working feed, then choose the quality that suits your home connection and Twin host.

If no picture appears, check that RTSP is enabled, the local camera account is correct, and the Twin host can reach the camera's address and port. When the camera sits behind a recorder, the URL may need the recorder's address, account, and channel instead.

A URL containing your camera password should stay private. Your camera and Twin communicate on the local network, so you do not need to publish the camera's RTSP port on the internet for Lens. Continue with [connection troubleshooting](access-and-troubleshooting.md) if the feed still fails.
