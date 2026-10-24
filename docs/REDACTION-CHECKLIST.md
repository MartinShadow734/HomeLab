# Redaction Checklist

This repository is public. Run through this list before committing any screenshot, photo, config, log, or diagram.

## Never publish

- [ ] Passwords, API keys, tokens, SSH private keys, recovery codes
- [ ] Public IP addresses
- [ ] Tailscale IPs, tailnet name, and Tailscale device names
- [ ] MAC addresses
- [ ] Serial numbers and service tags (on device labels, BIOS screens, Proxmox hardware views)
- [ ] Wi-Fi network names (SSIDs) and passwords
- [ ] Home address, location data, or photos that reveal where the lab is
- [ ] Usernames tied to real accounts
- [ ] Email addresses other than ones you intend to share
- [ ] Details of unresolved security investigations

## Photos from your phone

- [ ] **Remove location data.** On iPhone: tap Share, then Options at the top, then turn off Location before saving or sending. Photos otherwise carry GPS coordinates.
- [ ] Check the background for mail, documents, screens, or anything identifying
- [ ] Check device labels in the shot. Cover or crop serial numbers and MAC addresses

## Screenshots

- [ ] Crop to only what proves the point
- [ ] Blur or black out sensitive fields (a solid box is safer than blur)
- [ ] Check browser tabs, bookmarks bar, and URL bar
- [ ] Check terminal prompts for usernames and hostnames you don't want public

## Configs and command output

- [ ] Replace sensitive values with placeholders, for example `<REDACTED>` or `192.168.X.X`
- [ ] Private lab ranges like `10.10.20.0/24` are fine to show. They describe design, not your real home network
- [ ] Remove certificate contents and key fingerprints

## Final check

- [ ] Would I be comfortable if a hiring manager and an attacker both read this? If not, cut it.
