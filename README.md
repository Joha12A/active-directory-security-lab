# Active Directory Security Lab

This repository contains a hands-on Active Directory security lab built around a Windows Server domain environment, a Windows 10 client, and a Linux-based administration host.

## Objectives

- Model a realistic Active Directory environment for security exercises.
- Document architecture, configuration, and hardening steps.
- Practice detection, auditing, and remediation of AD security issues.
- Provide reusable scripts, configs, and notes for labs and demonstrations.

## Lab topology

- Domain Controller: `SRV-DC01` — Windows Server, AD DS + DNS
- Client: `CLIENT-W10` — Windows 10 joined to the domain
- Linux Server: `Ubuntu-Server` — future integration and automation host
- Host OS: Kali Linux + VirtualBox

## Repository structure

- `docs/` — technical documentation and lab notes
- `configs/` — AD, DNS, and GPO configuration files
- `scripts/` — PowerShell and Bash automation scripts
- `audit-reports/` — findings, reconnaissance, and remediation notes
- `screenshots/` — screenshots for each architecture step

## Documentation

- [docs/01-architecture/architecture.md](docs/01-architecture/architecture.md)
- [docs/02-active-directory/](docs/02-active-directory/)
- [docs/03-identity-management/](docs/03-identity-management/)
- [docs/04-access-control/](docs/04-access-control/)
- [docs/05-system-hardening/](docs/05-system-hardening/)
- [docs/06-dns-security/](docs/06-dns-security/)
- [docs/07-security-audit/](docs/07-security-audit/)
- [docs/08-remediation/](docs/08-remediation/)

## Notes

This environment is intentionally isolated for lab use and is designed for controlled security testing and documentation.
