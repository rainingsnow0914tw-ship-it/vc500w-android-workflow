# A practical VC-500W Android workflow

An experience-based guide to Brother VC-500W Wireless Direct, Android's no-internet Wi-Fi prompt, and printing artwork prepared outside Color Label Editor 2.

[繁體中文](README.zh-Hant.md)

This is an independent, experience-based guide, not Brother software or a firmware patch.

## What worked in this case

On a Galaxy S25 Ultra running Color Label Editor 2 version 1.1.6, the phone could join the printer's Wi-Fi but the app could not use the connection reliably. Selecting **Connect only this time** in Android's no-internet Wi-Fi dialog made the printer Wi-Fi the accepted default network. The app then connected and a read-only query on TCP 9100 returned a valid printer status.

This was followed by a 120-second screen-off test without phone/printer polling, an app restart, and two separately approved single-copy print jobs. Both prints were physically checked for output and cutting. These observations establish a working route for this setup; they do not establish the cause of every VC-500W disconnection.

## Quick start

1. Prepare and save the finished artwork while your phone has internet access. Download any assets before switching networks.
2. Check the actual cassette width and that the printer is ready. The example below used a 50 mm CZ roll.
3. Put the printer in **Wireless Direct mode (white Wi-Fi LED)** using the instructions for your model. Blue indicates infrastructure mode through a router.
4. In Android's normal Wi-Fi network list, select your printer's `Brother VC-500W XXXX` network. Verify the identifying suffix against your own printer.
5. If Android warns that this network has no internet, choose **Connect only this time**, **Stay connected**, or the equivalent on your phone. Our tested wording was Samsung's Traditional Chinese `僅此次連接`. Do not assume that association with the SSID means apps will use it.
6. Return to Color Label Editor 2 and wait for the printer/address to appear. A brief `Not connected` display can update after the network change. Inspect the current screen rather than repeatedly tapping.
7. Use **Photo → select the finished artwork → Orientation → Next → Option**. Check the complete preview and the copy count. For our landscape artwork, we selected **Horizontal**.
8. Send one copy, once. Observe the app and the physical printer before retrying any uncertain result.
9. Return the phone to its normal Wi-Fi when finished.

You do not need ADB, USB debugging, or a computer to follow these manual steps. If a developer-enabled phone asks to trust the printer network for wireless debugging, that is a separate permission and is not required for printing.

## Why prepare one finished image?

Designing the photo, background, lettering, and decorations together avoids repeated editing inside the label app. Keep the subject large enough for the small print, make shadow detail visible, and leave important content away from edges.

Our successful example was a 1536 × 1024 landscape image. A 3:2 image fitted with its short side across a 50 mm roll suggests an image area around 75 × 50 mm. This is a layout calculation, not a measured promise: printable area, margins, feed, and cutting can change the finished dimensions. Check the preview and measure a sample if exact dimensions matter.

Both comparison prints used one copy, **Vivid**, and **Auto** cutting. The brighter, larger-subject artwork was preferred in the physical comparison. We did not increase printer resolution or perform a calibrated color measurement. Vivid is a tested setting here, not a universal recommendation.

If you use generative image tools, an identity-preserving prompt is not pixel preservation: details may be redrawn. Use a composition workflow that leaves the photo layer unchanged when exact photographic fidelity matters.

## Troubleshooting by layer

| Observation | What it establishes | Next check |
|---|---|---|
| Phone lists the printer SSID | The network is visible | Join it and handle the no-internet prompt |
| Wi-Fi reports connected | Radio association / address assignment | Check the default network and app connection |
| Ping succeeds | Network reachability | Check the app/data channel |
| App says `Enable Port 9100` | The app wants that communication path | Verify routing and reachability before changing printer settings |
| TCP 9100 accepts a connection | Transport is reachable | A valid status response is stronger evidence than an open socket |
| App returns from printing | The UI flow ended | Check device result and the physical output |

In our case, an interface-bound ping worked while an ordinary ping failed. After the one-time no-internet acceptance, ordinary ping, TCP 9100, and the app worked. **The app's port warning did not prove that the port had been disabled.**

Samsung's **Switch to mobile data** option was already off in this case. We did not fix the connection by turning it off, disable mobile data, change router settings, enable ports, or install firmware. An enabled screen-off switch-to-better-Wi-Fi option also remained unchanged during the bounded test. Inspect your own settings; do not assume this case matches yours.

## Firmware and scope

No firmware was installed for this result. Public update filenames or `secure`/`v1` lists are not sufficient to choose a package for a specific printer. Follow the official update route and verify applicability; this guide does not distribute firmware or provide a downgrade procedure.

Not established: overnight reliability, battery-only deep standby, reliable infrastructure-mode recovery, other roll widths, other phone/software combinations, exact color fidelity, or exact finished dimensions. A local management-page certificate warning was not bypassed in the test.

## Sources

- [Brother mobile Wi-Fi connection instructions](https://help.brother-usa.com/app/answers/detail/a_id/163271/~/connect-the-label-printer-to-a-mobile-device-using-wi-fi)
- [Brother VC-500W user guide](https://download.brother.com/welcome/docp100376/vc500w_aus_ug_d01896001a.pdf)
- [Brother firmware update instructions](https://support.brother.com/g/b/sp/faqend.aspx?c=gb&faqid=faqp00100041_001&ftype3=100129&lang=en&prod=vc500weuk)
- [Brother color-mode adjustment](https://help.brother-usa.com/app/answers/detail/a_id/182610/~/adjust-the-color-mode-%E2%80%93-color-label-editor-2)
- [Samsung connection options](https://www.samsung.com/us/support/answer/ANS10002546/)
- [Color Label Editor 2 and first-person user reviews](https://play.google.com/store/apps/details?hl=en_AU&id=com.brother.ptouch.colorlabeleditor2)
- [Unofficial node-vc-500w project](https://github.com/honeymaro/node-vc-500w): contains an idle-disconnect / keep-alive suggestion for its own TCP client; it is not a patch to the Android app.

If sharing another result, include phone/OS, app version, connection mode, which layer failed, and the physical outcome. Remove serial numbers, SSIDs, addresses, account names, and personal photographs from diagnostic attachments. No proprietary firmware, private device logs, or user photos are included in this repository.
