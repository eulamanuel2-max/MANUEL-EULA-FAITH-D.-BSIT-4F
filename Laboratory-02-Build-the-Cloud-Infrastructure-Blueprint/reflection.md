# Reflection

## What I Did

For this exercise, I used the Killercoda Ubuntu playground — a free, browser-based Linux sandbox — to explore what actually makes up a cloud-hosted virtual machine. Instead of just reading about cloud infrastructure, I ran commands directly in the terminal to inspect the operating system, CPU, memory, and storage of the instance I was given: `cat /etc/os-release`, `uname -r`, `nproc`, `free -h`, `df -TH`, and `hostname`.

## What I Learned

- **Even a "free" sandbox is real infrastructure.** The environment wasn't just a simulation — it was an actual Ubuntu 24.04.4 LTS virtual machine with a real kernel (6.8.0-136-generic), a real allocated CPU core, real RAM, and a real virtual disk (`/dev/vda1`). Seeing the `vda` device naming made it click that this is backed by KVM/QEMU-style virtualization, the same technology real cloud providers use.
- **Resources are deliberately minimal.** With only 1 vCPU and ~2 GB of RAM, the sandbox is sized similarly to the smallest/free-tier instances on AWS, Azure, or GCP. This showed me that cloud providers scale resources up or down depending on the use case — a training sandbox doesn't need the same horsepower as a production server.
- **Cloud infrastructure is layered.** Underneath the friendly browser UI (Editor tab, session timer, Ask/Help panel), there's still a full Linux boot process — UEFI, GRUB, separate `/boot` and `/boot/efi` partitions — just like any real VM. The "cloud" experience is really just several layers (orchestration, virtualization, OS, storage, networking) stacked on top of each other, with the friendly UI hiding most of the complexity.
- **Ephemeral vs. persistent environments matter.** Because the session has a visible countdown timer, everything I did would disappear once it expired. That's very different from a production cloud VM, where storage and configuration persist until someone deliberately deletes it — a good reminder to always separate "throwaway" learning environments from "real" infrastructure I care about keeping.

## Challenges / Things I'd Do Differently

- I initially tried `hostname -H`, which isn't a valid flag — a small reminder to check `--help` or `man` pages instead of guessing flag names.
- I didn't capture networking details beyond the hostname (e.g., `ip a`, `hostname -I`). Next time, I'd also inspect the network interfaces to get a fuller picture of how the instance connects out to the internet.
- I'd like to repeat this same exercise on an actual free-tier AWS/Azure/GCP VM to directly compare the setup process, available commands, and resource limits against what Killercoda offers "for free."

## Why This Matters

This exercise reinforced that "the cloud" isn't magic — it's just someone else's well-managed hardware, abstracted through virtualization and orchestration layers so it feels instant and disposable. Understanding the building blocks (compute, memory, storage, OS, networking) at this small scale makes it much easier to reason about how much larger, production cloud systems are architected.
