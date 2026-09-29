# System Architecture

## Purpose

Oslo Homelab provides shared storage and self-hosted services for me,
household members, and family. I built it to expand beyond my main PC's
storage and to develop hands-on systems administration skills.

## Hardware

| Component | Current configuration |
| --- | --- |
| Motherboard | ASUS PRIME B560M-A |
| CPU | Intel Core i7-10700K |
| RAM | 32 GB |
| Boot drive | Acer SSD FA100 256GB NVMe |
| HDDs | 4 × WD Red WD80EFPX 8TB |
| Application SSDs | 2 × Crucial BX500 2TB SATA SSDs |
| Network adapter | Intel I219-V Ethernet |
| GPU | RTX 2080 Ti |

## Storage layout

| Pool | Configuration | Purpose |
| --- | --- | --- |
| `Oslo Homelab` | 4 × 8TB HDDs in RAIDZ1 | Media, general storage, PC backup files, and VM installation images |
| `SSDapps` | 2 × 2TB SSDs in a mirror | Applications, configuration data, and game-server files |
| `boot-pool` | Acer 256GB NVMe | TrueNAS operating system |

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
