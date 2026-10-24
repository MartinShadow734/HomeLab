# Adding Photos and Screenshots

How to add images to this repo from a phone, with nothing but a browser.

## Where images go

Each project keeps its own images next to its write-up:

```
projects/
  01-proxmox-virtualization/
    README.md
    images/
      proxmox-dashboard.png
      vm-list.png
```

Rack photos and the lab overview go in the repo root `images/` folder. Network diagrams go in `diagrams/`.

## File naming

- Lowercase, words separated by hyphens: `rack-front.jpg`, `vlan-table.png`
- Describe what the image shows, not when it was taken. Avoid names like `IMG_9223.png`
- Keep images under about 1 MB when you can. Large phone photos slow the page down

## Upload from your phone

1. Run the photo through the [redaction checklist](REDACTION-CHECKLIST.md). Turn off location data first.
2. Rename the photo if you can (the Files app works for this).
3. On github.com, open the target `images/` folder.
4. Tap **Add file**, then **Upload files**. If you don't see it, request the desktop site.
5. Choose **Create a new branch for this commit and start a pull request**, so changes get reviewed before going live.
6. Commit.

## Show the image in a write-up

Add a line like this to the project README, using a path relative to that README:

```markdown
![Proxmox dashboard showing all running VMs](images/proxmox-dashboard.png)
```

The text in brackets is alt text. Describe what the image proves, for example "VLAN-aware bridge enabled on vmbr0," not just "screenshot."
