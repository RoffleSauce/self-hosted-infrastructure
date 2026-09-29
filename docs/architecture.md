# Oslo Homelab: System Architecture

## Project purpose

Oslo Homelab is a TrueNAS SCALE home server I built to expand storage beyond my main PC and develop hands-on systems administration skills. It provides file storage and self-hosted services for me, household members, and family.

The project began with a smaller HDD pool and has grown to support PC backups, media streaming, a virtual machine, dedicated game servers, and other self-hosted applications. This document describes the server's hardware, storage, and network architecture and how they have changed over time.

## Current hardware

| Component | Configuration |
| --- | --- |
| Case | Rosewill RSV-Z3200U 3U rackmount server chassis |
| Motherboard | ASUS PRIME B560M-A |
| CPU | Intel Core i7-10700K |
| RAM | 32 GB across two modules |
| Power supply | EVGA 750 G3 |
| Boot drive | Acer SSD FA100 256GB NVMe |
| HDDs | 4 × WD Red WD80EFPX 8TB |
| Application SSDs | 2 × Crucial BX500 2TB SATA SSDs |
| GPU | RTX 2080 Ti |
| Managed switch | Netgear ProSAFE Plus JGS524E |
| Wired network adapter | Intel I219-V Ethernet |

The server runs TrueNAS SCALE 25.10.7. It is housed in a rackmount chassis and connects to the home network by Ethernet through the managed switch.

## Storage architecture

| Pool | Configuration | Primary use |
| --- | --- | --- |
| `boot-pool` | Acer 256GB NVMe | TrueNAS operating system |
| `Oslo Homelab` | 4 × 8TB HDDs in one RAIDZ1 vdev | Media, general files, PC backups, and VM installation images |
| `SSDapps` | 2 × 2TB SSDs in one mirror vdev | Applications, configuration data, and game-server files |

I keep large media files and general storage on the HDD pool. I added a separate mirrored SSD pool for application workloads and their associated files.

### HDD pool datasets

| Dataset | Purpose |
| --- | --- |
| `media` | Videos, audio, and other files used by Jellyfin |
| `Storage` | General files and Windows PC backup files |
| `Virtual_Disks` | Installation images for virtual machines |
| `SSDapps-backup` | Destination for a one-time copy of SSD application data made while investigating a drive fault |

### SSD pool datasets

| Dataset | Purpose |
| --- | --- |
| `application` | Application storage |
| `config` | Application configuration files |
| `Game_server` | Dedicated game-server files |

Selected datasets are accessible through SMB shares. Share access and permissions will be covered in the storage documentation.

## Network architecture

The server has a static IP address and connects by Ethernet to a Netgear ProSAFE Plus JGS524E managed switch. A network bridge is used by the Kali Linux virtual machine.

I use Tailscale for remote access to the server and selected services. I also use Cloudflare for selected application access and DNS. The access path for each service will be covered in separate networking and applications documentation.

VLANs are not currently in use on this server connection.

## Hardware evolution

I completed a major hardware upgrade in July 2026 to increase storage capacity and support more applications.

| Component | Original build | Current build |
| --- | --- | --- |
| Motherboard | ASUS ROG STRIX Z270H GAMING | ASUS PRIME B560M-A |
| CPU | Intel Core i7-7700K | Intel Core i7-10700K |
| RAM | 32 GB across four modules | 32 GB across two modules |
| HDD pool | 4 × WD Red WD40EFRX 4TB | 4 × WD Red WD80EFPX 8TB |
| Application SSD pool | Not present initially | 2 × Crucial BX500 2TB SSDs in a mirror |
| Dedicated GPU | None | RTX 2080 Ti |

I upgraded the CPU and motherboard as I planned to run more applications. I expanded the HDD pool after PC backups and other files brought the original pool to approximately 75% usage. I added separate SSD storage for application workloads and added the GPU for media and local AI workloads.

The original four WD Red 4TB HDDs are set aside. I plan to reuse them if I move to a motherboard and case with room for four additional drives; a hot-swappable case is a feature I would like in that future build. I also plan to add two more RAM modules to increase total memory from 32 GB to 64 GB.

## Workloads

Oslo Homelab supports:

- General file storage and selected SMB shares.
- Jellyfin media storage and streaming.
- A Kali Linux virtual machine for cybersecurity learning activities.
- Dedicated game servers that can remain available without running my main PC.
- Other self-hosted applications for travel planning, fitness tracking, video downloads, network services, storage monitoring, and local AI experimentation.

Application-specific deployment steps and access methods will be documented in separate pages.
