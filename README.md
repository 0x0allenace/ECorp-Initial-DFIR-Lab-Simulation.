# Initial  ECorp DFIR Lab (LAN Simulation)

**Goal:** Simulate a centralized DFIR environment for a small corporate LAN using PfSense, Windows AD, Velociraptor, and a Kali attacker host.

## What this repo contains
- Documentation for the lab topology and step-by-step setup (`/docs`)
- Example configs for Velociraptor and PfSense (`/configs`)
- Useful VQL (Velociraptor Query Language) hunts (`/vql`)
- Scripts to automate common tasks (`/scripts`)
- Placeholder for screenshots (`/screenshots`)
- Incident response checklist template (`/templates`)

## Quick start
1. Clone the repo:
   ```bash
   git clone https://github.com/<your-user>/ecorp-dfir-lab.git
   cd ecorp-dfir-lab

2. Add your screenshots to /screenshots (names should match examples or update README).

3. Edit configs/velociraptor-server.conf.example -> save as velociraptor-server.conf and customize as needed.

4. Follow detailed steps in /docs to spin up VMs and configure PfSense and Active Directory.

Push to GitHub

git init
git add .
git commit -m "Initial ECorp DFIR lab repo"
git remote add origin git@github.com:<your-user>/ecorp-dfir-lab.git
git branch -M main
git push -u origin main

Licensing

See LICENSE in repository (MIT by default).


Example files (snippets)

scripts/windows/join-domain.ps1

# join-domain.ps1
param(
  [string]$Domain = 'ECorp.local',
  [string]$OU = 'OU=Employees,DC=ECorp,DC=local',
  [string]$AdminUser = 'ECorp\\Administrator',
  [string]$AdminPass = 'P@ssw0rd!'
)

$securePass = ConvertTo-SecureString $AdminPass -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential($AdminUser, $securePass)
Add-Computer -DomainName $Domain -Credential $cred -OUPath $OU -Restart

Note: Replace plaintext password usage with secure credential distribution (e.g., LAPS, Secret store) before production use.

configs/velociraptor-server.conf.example


# Velociraptor server minimal snippet
server:
  listen: '0.0.0.0:8000'
  ssl_cert: '/etc/velociraptor/server.crt'
  ssl_key: '/etc/velociraptor/server.key'
  datastore:
    type: sqlite
    location: '/var/lib/velociraptor/velociraptor.db'

# Adjust for your lab and register clients with correct backend settings.

vql/quick-hunt-queries.vql

# Example VQL: list running suspicious processes
SELECT * FROM running_processes() WHERE name LIKE '%powershell%' OR name LIKE '%rundll32%'

# Example VQL: find persistence via scheduled tasks
SELECT * FROM scheduled_tasks() WHERE Action LIKE '%powershell%' OR Author LIKE '%SYSTEM%'


scripts/linux/collect-host-info.sh

#!/usr/bin/env bash
# collect-host-info.sh - lightweight host info collector
uname -a > /tmp/host-info.txt
ss -tunap >> /tmp/host-info.txt
ps aux --sort=-%mem | head -n 50 >> /tmp/host-info.txt

docs/overview (briefs)

docs/lab-topology.md — Visual diagram instructions and IP plan (include your pfSense static mapping screenshot here).

docs/ad-setup.md — Step-by-step AD roles and OU/GPO recommendations.

docs/pfsense-setup.md — How to set static DHCP, firewall rules to segment AttackLAN vs CorpLAN.

docs/velociraptor-setup.md — Server and agent registration steps, sample VFS/flow configs, and tips for creating artifacts.

Incident Response Checklist (templates/incident-response-checklist.md)

A short checklist to use during a tabletop or live incident:

Identify affected hosts

Isolate from network (if necessary)

Collect volatile data (memory, processes, network connections)

Pull relevant logs from Velociraptor

Capture disk images if required

Remediate and re-image compromised hosts

Post-incident review & update detections

How to add your screenshots

Place images inside /screenshots/ and keep filenames descriptive.

Reference them in docs/ using relative paths, e.g.: ![PfSense DHCP](/screenshots/01_pfsense_dhcp.png)
