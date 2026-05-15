# 🚀 Hexcore Lab: Raspberry Pi 5 Homelab

Este repositório centraliza a infraestrutura, automações e registros do meu laboratório pessoal. O projeto foca na transição para a **cultura DevOps**, aplicando conceitos de **IaC** (Infrastructure as Code), segurança ofensiva/defensiva e monitoramento contínuo.

---

## 🛠️ Hardware & Host
A base do projeto é um Raspberry Pi 5, configurado para alta performance e estabilidade.

* **Processador:** Broadcom BCM2712 (Cortex-A76)
* **Memória:** 16GB LPDDR4X
* **Armazenamento:** SSD NVMe (via PCIe)
* **Case:** Pironman 5 (Status OLED)
* **SO:** Raspberry Pi OS 64-bit (Debian Bookworm)

---
## 🏗️ Arquitetura de Software & DevOps
A infraestrutura é modular e isolada, permitindo deploys rápidos e versionamento completo.

| Camada | Tecnologia | Função |
| :--- | :--- | :--- |
| **Container Engine** | Docker | Isolamento de processos |
| **Orquestração** | Docker Compose | Declaração de Infraestrutura (IaC) |
| **Gestão Visual** | Portainer | Monitoramento de containers e recursos |
| **Rede/VPN** | Tailscale | VPN Mesh (Zero Trust) sem portas expostas |
| **Versionamento** | Git/GitHub | Documentação e histórico de alterações |

### 🔒 Segurança (Hardening)
- **SSH:** Autenticação via Chaves Ed25519 (Passwordless) e login de Root desativado.
- **Secrets Management:** Uso de `secrets.yaml` e `.gitignore` para proteção de tokens e senhas.
- **Network:** Acesso externo restrito à rede privada via Tailscale.

---

## 📦 Serviços em Rodando (Stack)
- **Home Assistant:** Central de automação inteligente.
- **Portainer:** Dashboard de gerenciamento Docker.

---

## 🛡️ Registro de Incidentes (Post-Mortem)
Documentação técnica de falhas para base de conhecimento e Troubleshooting.

### 🔴 Incidente 001: File System Read-only Lock
**Data:** 14/05/2026 | **Severidade:** Alta

**Sintoma:** Bloqueio de escrita na partição `/boot/firmware` impedindo o upgrade do Kernel (`initramfs-tools`).

**Causa Raiz:** Inconsistência lógica durante escrita de firmware; mecanismo de proteção do Kernel ativado para evitar corrupção de dados.

**Resolução:**
1. Remontagem forçada da partição: `sudo mount -o remount,rw /boot/firmware`
2. Reparo de dependências: `sudo dpkg --configure -a`

**Lição Aprendida:** Importância de monitorar o estado de montagem do SSD e validar a integridade após atualizações críticas de firmware.

---

## 📈 Próximos Passos
- [ ] Implementar monitoramento de temperatura do Pi via Home Assistant.
- [ ] Configurar Backup automatizado dos volumes Docker para o Cloud.
- [ ] Implementar Nginx Proxy Manager para gestão de subdomínios internos.
