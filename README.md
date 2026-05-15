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


🛡️ Registro de Incidentes

Nesta seção, documento os desafios técnicos encontrados durante a manutenção do laboratório, servindo como base de conhecimento e portfólio de Troubleshooting.

🔴 Incidente 001: Bloqueio de Escrita no Sistema de Arquivos (Read-only)
**Data:** 14 de Maio de 2026  
**Severidade:** Alta (Impediu atualizações de segurança e causou falha no login do Home Assistant)

📝 Descrição do Problema
Durante a atualização do Kernel e Firmware do Raspberry Pi 5, o sistema entrou em modo **Read-only** (Somente Leitura) na partição `/boot/firmware`. Isso resultou em falhas críticas nos pacotes `initramfs-tools` e `raspi-firmware`, impedindo a inicialização correta de novos módulos do sistema.

🔍 Causa Raiz
Inconsistência lógica no sistema de arquivos durante o processo de escrita do Kernel. O Linux bloqueou a escrita para evitar a corrupção total dos dados de boot, um mecanismo de proteção comum quando há falhas de montagem ou setores instáveis no armazenamento.

🚀 Resolução e Recuperação
Para solucionar o incidente, segui os seguintes passos de infraestrutura:
1. **Remontagem Manual:** Forcei a partição a aceitar escrita novamente:
   ```bash
   sudo mount -o remount,rw /boot/firmware
