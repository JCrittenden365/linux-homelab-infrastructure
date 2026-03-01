# Lessons Learned

## Overview

This document summarizes the broader takeaways from building the lab — things that cut across multiple topics and shaped how the project evolved. Specific technical lessons are noted at the end of each individual document.

---

## 1. Hands-On Work Reveals What Reading Doesn't

Documentation and tutorials explain how things should work. Actually configuring them reveals edge cases, permission quirks, and sequencing dependencies that don't show up in guides. Every issue in the [Troubleshooting Journal](troubleshooting-journal.md) was more educational than the configuration that preceded it.

---

## 2. Order of Operations Matters

Several tasks have a specific sequence that must be followed:

- SSH keys must be working **before** disabling password authentication
- SSH must be allowed in UFW **before** enabling the firewall
- `sudo sshd -t` must pass **before** restarting the SSH service

Getting the order wrong in any of these can lock you out of the system.

---

## 3. Layered Security Is More Than a Concept

Implementing SSH hardening, UFW, and Fail2Ban individually made sense on paper. Seeing them interact — Fail2Ban writing ban rules through UFW, logs showing blocked IPs, the Fail2Ban status reflecting real-time jail state — made the concept of defense-in-depth concrete rather than theoretical.

---

## 4. Documentation Is Part of the Work

Writing these docs while configuring the systems reinforced the material and exposed gaps in understanding. If a step couldn't be explained clearly, it usually meant it wasn't fully understood yet.

---

## 5. The Lab Is a Safe Place to Break Things

Every misconfiguration here is a lesson with no consequences beyond a VM reboot. The goal was to encounter real problems in a safe environment — and that happened repeatedly. That's the point.

---

## Future Directions

- Centralized logging (currently planned)
- Automated backups with verification
- Docker container deployment
- Infrastructure as Code (Ansible or Terraform)
- Monitoring with Prometheus and Grafana
