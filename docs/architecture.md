# System Architecture

## Purpose

Oslo Homelab provides shared storage and self-hosted services for me,
household members, and family. I built it to expand beyond my main PC's
storage and to develop hands-on systems administration skills.

## Hardware

| Component | Current configuration | Why I chose or upgraded it |
| --- | --- | --- |
| CPU | To add | More processing capacity for additional applications |
| Motherboard | To add | Replaced to support the upgraded CPU |
| RAM | To add | Future upgrade planned |
| Boot drive | Acer SSD FA100 256GB NVMe | TrueNAS boot device |
| HDDs | Four WD Red NAS 8TB drives | Expanded capacity after the original pool reached about 75% usage |
| SSDs | To confirm | Separate, faster storage for applications |
| GPU | RTX 2080 Ti | Jellyfin transcoding and LocalAI experimentation |
| Network | Ethernet connection through a managed switch | Wired connectivity for the server |

## Storage layout

| Pool | Layout | Main purpose |
| --- | --- | --- |
| Oslo Homelab | Four-drive RAIDZ1 HDD pool | Media, general storage, PC backup files, and VM installation images |
| SSDapps | Two-drive mirrored SSD pool | Applications, configuration data, and game servers |

### HDD pool datasets

- `media`: Videos, audio, and other files used by Jellyfin.
- `Storage`: General files and Windows PC backup files.
- `Virtual_Disks`: Installation images for virtual machines.
- `SSDapps-backup`: Dataset intended for copies of SSD application data; backup task and restore status to be confirmed.

### SSD pool datasets

- `application`: Application storage.
- `config`: Application configuration files.
- `Game_server`: Dedicated game-server files.

## Network overview

The server connects by Ethernet to a managed switch on my home network.
I use a static address for the server and Tailscale for remote access.
Selected services also use Cloudflare.

<!-- To add: a sanitized diagram showing the server, switch, home devices,
     remote users, and the different remote-access paths. -->

## Design decisions

- I placed large media and general-purpose files on HDD storage.
- I added separate SSD storage for applications.
- I separated workloads into datasets so I can manage their storage and access independently.
- I expanded HDD capacity as PC backups and other files filled the original pool.

## Changes over time

1. Built the initial TrueNAS server with a boot drive and four 4TB HDDs.
2. Expanded the HDD pool to four 8TB drives.
3. Added separate SSD storage for applications.
4. Upgraded the CPU and motherboard to support additional workloads.
5. Added a GPU for Jellyfin and LocalAI use.

<!-- Check the order above and add dates only if you know them. -->
