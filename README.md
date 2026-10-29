# InspectryxIQ

**The Infrastructure PACS.** One permanent diagnostic record for every asset you own, with the intelligence, evidence and dollars computed from it. Published by Amhage Technology Group LLC, Rochester, New York.

This repository holds the public releases of the **InspectryxIQ On-Premises Edition**: installers, deployment files, the virtual appliance, manuals and checksums. The hosted platform is at [app.inspectryxiq.com](https://app.inspectryxiq.com).

## Overview

Healthcare solved enterprise imaging decades ago with PACS: every study kept for the life of the patient, readable on any workstation, signed and auditable. InspectryxIQ applies that model to infrastructure. The asset is the patient. An inspection is a study. CCTV sewer video, culvert and bridge photography, facade and asbestos surveys, drone sets, NDT radiography and ultrasound, thermal and LiDAR all land in one standards-based archive (DICONDE at the core), with findings graded G1 to G5, reports that seal an evidence manifest, and a verification link anyone can check.

Built for public agencies, water and wastewater utilities, DOTs, engineering and inspection firms, and NDT labs.

## Editions

| Edition | Price | What you get |
|---|---|---|
| **On-Premises Edition** | Free | The full platform on your own hardware. No account, no time limit, no data leaves the building. Deployment files GPLv2. |
| **Support Plan** | $199 / month | Business-hours support by email, upgrade guidance, configuration and performance tuning. Cancel any time. |
| **Professional Install** | $499 one time | Remote installation on your hardware or hypervisor and first-day configuration: users, assets, watched folder or equipment, backups. |
| **Managed Cloud** | from $3,900 / year | We run it: hosted, backed up, upgraded, with a tenant address of your own. Tiers for practices, municipalities and enterprises at [inspectryxiq.com](https://inspectryxiq.com/#pricing). |

Card checkout, no contract: [inspectryxiq.com/services](https://inspectryxiq.com/services/) and [inspectryxiq.com/upgrade](https://inspectryxiq.com/upgrade/).

## What is included

Assets registry with history · Inspections with media, findings and PACP-style coding · Worklist and diagnostic Workstation (measure, annotate, grade) · Field Kit for phones and tablets · Schedule, Fleet Risk and Capital Plan · Work Orders · Delivery Exchange for contractors with QA · Map · Compliance and append-only Audit Log · Imaging archive browser (DICONDE/DICOMweb) · Reports with draft, final, amended lifecycle · Evidence manifests and public verification · Watched-folder and DICOM receive · Roles (Viewer, Inspector, Manager, Admin) and client-portal users · Branding · Second factor · Sealed-network operation.

## System requirements

| | Minimum | Recommended |
|---|---|---|
| Windows | Windows 11 64-bit, 2 cores, 8 GB RAM, 60 GB free disk | 16 GB RAM, SSD |
| Linux | 64-bit, Docker Engine 24+ with Compose v2, 2 cores, 8 GB RAM, 60 GB disk | 16 GB RAM, SSD |
| Appliance | VirtualBox 7, VMware or Proxmox; 2 vCPU, 8 GB RAM, 60 GB disk | Bridged network, fixed address |
| Browser | Current Chrome, Edge, Firefox or Safari | |

Internet is needed for the first start (image download) and upgrades only. Measured on the 1.0.0 appliance: the five images total 4.1 GB (imaging engine 2.6 GB, application 0.8 GB, database 0.4 GB, front end and proxy 0.2 GB); a fresh install uses 6.7 GB of disk including the OS and under 1 GB of memory at idle. The 60 GB is headroom for your archive. The hosted platform runs the same images on a 2 vCPU, 4 GB server.

## Deployment

**Windows installer.** Download `InspectryxIQ-Setup.exe` from the [latest release](https://github.com/Amhage-Technology-Group/inspectryxiq-releases/releases/latest), run it, follow the prompts. Docker Desktop is installed if missing. The console opens at `https://inspectryxiq.localhost/` on a setup page where you create your organization and administrator. Re-run a newer installer to upgrade; data, settings and users are kept.

**Virtual appliance.** Import `InspectryxIQ-Appliance-1.0.0.ova` (Ubuntu 24.04 LTS), set the network adapter to Bridged, power on. First boot needs internet and about ten minutes; the VM screen then shows the console address. Shell `inspectryxiq` / `inspectryxiq`, change forced at first login.

**Docker Compose.** Unzip `inspectryxiq-deploy-v1.0.0.zip` on a Linux host with Docker and run `sudo bash up.sh`. The first run generates secrets, pulls images, migrates the schema and prints the console address. `up.sh --pull` upgrades in place.

All three produce the same console from the same images: `ghcr.io/amhage-technology-group/inspectryxiq-backend` and `inspectryxiq-frontend`, plus PostgreSQL 17, the Orthanc imaging engine and Caddy.

## Documentation

| Manual | Pages | For |
|---|---|---|
| [Quick Start Guide](https://github.com/Amhage-Technology-Group/inspectryxiq-releases/releases/latest/download/InspectryxIQ-Quick-Start-Guide-1.0.0.pdf) | 3 | Download to a sealed, verifiable report in about fifteen minutes |
| [Installation Guide](https://github.com/Amhage-Technology-Group/inspectryxiq-releases/releases/latest/download/InspectryxIQ-Installation-Guide-1.0.0.pdf) | 12 | Every platform; networking, certificates, equipment, upgrades, backup, troubleshooting |
| [Administrator Guide](https://github.com/Amhage-Technology-Group/inspectryxiq-releases/releases/latest/download/InspectryxIQ-Administrator-Guide-1.0.0.pdf) | 7 | The console, users and roles, data, reports and evidence, security practices, support |

## Security model

Only TCP 80 and 443 are published; database, imaging engine and application are reachable only inside the stack. HTTPS is on from the first start through a per-install certificate authority (trust `ca.crt` on client PCs, or bring your own certificate). Every secret is generated on your machine at first start and lives in one file, `.env`. Writes are role-gated; reads require sign-in; a second factor can be required for writes. Every media item is hashed on arrival; final reports seal a hashed manifest; verification recomputes from stored bytes. DICOM receive is closed until three deliberate steps open it. After the first start the platform needs no internet except, optionally, map base imagery.

## Verifying downloads

Every release ships `SHA256SUMS.txt`. Windows: `certutil -hashfile InspectryxIQ-Setup.exe SHA256`. Linux and macOS: `sha256sum -c SHA256SUMS.txt`. The Windows binaries are not yet code-signed; the checksum is the verification.

## Support and services

| Channel | Scope |
|---|---|
| [Issues](https://github.com/Amhage-Technology-Group/inspectryxiq-releases/issues) | Defects and installation problems with the free edition |
| support@inspectryxiq.com | Support Plan customers; security reports |
| [inspectryxiq.com/services](https://inspectryxiq.com/services/) | Support Plan, Professional Install |
| [inspectryxiq.com/upgrade](https://inspectryxiq.com/upgrade/) | Managed Cloud |

Mirror: [sourceforge.net/projects/inspectryxiq](https://sourceforge.net/projects/inspectryxiq/)

## Licensing and trademarks

The deployment files in each release (installer, Compose definitions, proxy and imaging-engine configuration, scripts, appliance build files) are licensed under the GNU General Public License v2 ([COPYING](https://github.com/Amhage-Technology-Group/inspectryxiq-releases/blob/main/COPYING)). The application images are distributed free of charge for use with them; third-party components (Orthanc, PostgreSQL, Caddy, nginx and others) remain under their own licenses. InspectryxIQ and the reticle mark are trademarks of Amhage Technology Group LLC; see [TRADEMARKS.md](https://github.com/Amhage-Technology-Group/inspectryxiq-releases/blob/main/TRADEMARKS.md). Terms of use: [TERMS.md](https://github.com/Amhage-Technology-Group/inspectryxiq-releases/blob/main/TERMS.md).

## About Amhage Technology Group

Amhage Technology Group LLC is a Rochester, New York software company built on two decades of medical imaging PACS experience. It publishes InspectryxIQ (the Infrastructure PACS), AeryxIQ (Drone PACS) and NeuryxIQ (autonomous security for medical and dental practices). hello@inspectryxiq.com
