Raspberry Pi 5 - Homelab

Este repositório contém a documentação e os arquivos de configuração do meu laboratório pessoal. O foco deste projeto é a migração para a cultura DevOps, aplicando automação, segurança e monitoramento.

🛠️  Hardware Processador: Broadcom BCM2712 (Raspberry Pi 5)

Memória: 16GB LPDDR4X

Armazenamento: SSD NVMe (via interface PCIe)

Estou utilizando a case Pironman 5 (Cooler + Led de status)

🏗️  Arquitetura de Software

A infraestrutura é baseada em containers, garantindo isolamento e portabilidade dos serviços.

SO: Raspberry Pi OS 64-bit (Debian Bookworm)

Orquestração: Docker & Docker Compose

Acesso Seguro: SSH Hardening (Ed25519 Keys + Passwordless)

Rede: VPN Mesh (Tailscale) para acesso remoto seguro sem exposição de portas.
