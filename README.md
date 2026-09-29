# Home Server Portfolio

## Overview

Oslo Homelab is a personal TrueNAS SCALE project I built to expand storage beyond my main PC and gain hands-on experience with systems administration. It began as a way to access files locally and remotely and has grown into a home server used by me, household members, and family.

The server supports file storage and PC backups, Jellyfin media streaming, virtual machines, dedicated game servers, and other self-hosted applications. This repository documents how I designed, configured, maintained, and troubleshot the system.

## What I worked on

- Built and upgraded a TrueNAS SCALE server as storage and application needs grew.
- Organized HDD and SSD storage into separate pools and datasets for media, general files, applications, and game servers.
- Configured SMB file sharing for access to selected datasets.
- Deployed applications and dedicated game servers, including custom YAML/Compose configurations.
- Configured remote access using Tailscale and Cloudflare for different services.
- Investigated storage, network, and application issues using TrueNAS tools, logs, and the shell.

## Current architecture

| Component | Purpose |
| --- | --- |
| TrueNAS SCALE 25.10.7 | Server operating system and management platform |
| Four-drive RAIDZ1 HDD pool | Media, general storage, PC backup files, and VM installation images |
| Two-drive mirrored SSD pool | Applications, configuration data, and game-server files |
| Managed network switch | Wired connection between the server and home network |
| RTX 2080 Ti | Jellyfin transcoding and LocalAI experimentation |

## Services

- **Jellyfin:** Media access for household members and family.
- **Tailscale:** Remote access to the server and selected services.
- **Cloudflare:** Remote access for selected web applications and DNS for selected services.
- **Virtual machines:** A Kali Linux VM used for cybersecurity learning activities.
- **Dedicated game servers:** Multiplayer servers that can remain available without running my main PC.
- **Other self-hosted applications:** AdventureLog, MeTube, Pi-hole, Scrutiny, SparkyFitness, LocalAI, and NPMplus.

## Project goals

This project helps me practice storage administration, networking, application deployment, access management, troubleshooting, and technical documentation. I am documenting not only the working configuration, but also the decisions and problems involved in maintaining it.

## Documentation status

Detailed architecture notes, build procedures, and troubleshooting case studies are in progress. I will add links here as those documents are completed.
