# Rerinku View for Unraid

Community Applications template for [Rerinku View](https://rerinku.com), a self-hosted NVR for ONVIF, RTSP and GB28181 cameras.

The templates in this repository are MIT licensed. The Rerinku View container image (`ghcr.io/rerinku/view`, also on Docker Hub as `rerinku/view`) is freeware and has its own terms; it bundles FFmpeg (GPLv3) and frp (Apache-2.0).

## Install

Search for **Rerinku View** in Apps, then Install. Open the WebUI and add cameras under Devices.

## Notes

- **Host networking.** The template uses host networking: WebRTC uses ephemeral UDP ports, and GB28181 (5060) and the device MQTT broker (1883) must be reachable on the server's address. Make sure 8080, 1883 and 5060 are free, or change the console port with `HTTP_ADDR`.
- **Permissions.** The container runs as `PUID=99` / `PGID=100` (nobody:users), as other Unraid containers do. On start it hands the appdata and recordings folders to that user, once, so a folder created by Docker as root works too. This needs image 0.1.1 or newer.
- **Recordings.** Point the Recordings path at a share on the array or a large pool. Keep Appdata on a cache or SSD pool.
- **GPU decoding (optional).** Add `/dev/dri` in the GPU field for Intel or AMD hardware video decoding. NVIDIA needs the Nvidia Driver plugin and extra parameters `--runtime=nvidia` plus the `NVIDIA_VISIBLE_DEVICES` variable.
- **USB cameras.** Pass the device with an extra Device entry, for example `/dev/video0`.
- **Security.** The console has no accounts, only an optional access password (Settings). Set it before exposing the port beyond your LAN, and do not forward it to the internet without a TLS reverse proxy.

## Support

https://github.com/rerinku/rerinku-view/issues
