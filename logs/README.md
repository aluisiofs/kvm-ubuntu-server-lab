# 🚀 KVM + Ubuntu Server 24.04 Lab

![Linux](https://img.shields.io/badge/OS-Linux-blue?logo=linux)
![KVM](https://img.shields.io/badge/Virtualization-KVM-red)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04_LTS-orange?logo=ubuntu)
![Status](https://img.shields.io/badge/status-active-success)
![Security](https://img.shields.io/badge/security-best_practices-green)

---

Projeto prático de virtualização utilizando **KVM/QEMU** no Linux (Pop!_OS), com criação e configuração de uma VM Ubuntu Server 24.04 LTS e acesso remoto via SSH.

---

## 🖥️ Arquitetura do Ambiente

![Diagrama](docs/diagrama-kvm.png)

---

## 🔐 Segurança

> ⚠️ Este projeto segue boas práticas de cibersegurança:

* IPs anonimizados (`192.168.X.X`)
* Usuários genéricos (`user`)
* Nenhuma credencial exposta
* Estrutura segura para publicação pública

---

## ⚙️ Stack utilizada

* Linux (Pop!_OS Host)
* KVM / QEMU
* libvirt
* virt-manager
* Ubuntu Server 24.04.4 LTS
* OpenSSH

---

# 🔧 1. Instalação completa do ambiente KVM (HOST)

## Atualização do sistema

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Instalação dos pacotes de virtualização

```bash
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager -y
```

---

## Verificar suporte à virtualização

```bash
lsmod | grep kvm
```

Saída esperada:

```bash
kvm_amd ou kvm_intel
kvm
```

---

## Ativar e iniciar serviço libvirt

```bash
sudo systemctl enable --now libvirtd
```

Verificar status:

```bash
systemctl status libvirtd
```

---

# 🌐 2. Configuração da rede virtual (NAT)

```bash
sudo virsh net-start default
sudo virsh net-autostart default
```

---

## Verificar rede

```bash
ip a | grep virbr0
```

Saída esperada:

```bash
192.168.122.1/24
```

---

# 🖥️ 3. Criação da Máquina Virtual

Configurações utilizadas:

| Recurso | Valor                     |
| ------- | ------------------------- |
| ISO     | Ubuntu Server 24.04.4 LTS |
| RAM     | 4GB+                      |
| CPU     | 2                         |
| Disco   | 25GB                      |
| Rede    | NAT (virbr0)              |
| Driver  | VirtIO                    |

---

## ⚠️ Ajuste importante (erro OpenGL)

Caso ocorra erro:

```bash
opengl is not available
```

### Solução:

* Alterar vídeo para **VirtIO**
* Desativar aceleração 3D

---

# 🧪 4. Testes de conectividade (HOST)

```bash
ip a
ping 192.168.122.X
```

---

# 🔐 5. Acesso remoto via SSH

```bash
ssh user@192.168.122.X
```

---

# 🖥️ 6. Configuração do Ubuntu Server (VM)

## Atualizar sistema

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Testar conectividade externa

```bash
ping -c 6 google.com
```

---

## Verificar IP da VM

```bash
ip a
```

---

## Instalar e ativar SSH

```bash
sudo systemctl enable --now ssh
```

---

## Verificar serviço SSH

```bash
sudo systemctl status ssh
```

---

## Verificar porta 22

```bash
sudo ss -tulpn | grep :22
```

---

## Verificar comunicação com host

```bash
ping -c 7 192.168.122.1
```

---

## Verificar leases DHCP

```bash
sudo virsh -c qemu:///system net-dhcp-leases default
```

---

## Renovar IP

```bash
sudo dhclient
```

---

# ⚠️ Problemas e correções

## ❌ SSH não conecta

### Causa:

Serviço SSH não ativo

### Solução:

```bash
sudo systemctl enable --now ssh
```

---

## ❌ Erro de hostname

```bash
ssh user@192.168.122.X/24
```

### Correto:

```bash
ssh user@192.168.122.X
```

---

## ❌ Sem internet na VM

### Verificar:

```bash
ip a
ping 192.168.122.1
```

---

# 📸 Evidências

![Host](docs/ip-host.png)
![Ping](docs/ping-vm.png)
![SSH](docs/ssh-login.png)

---

# 📂 Logs

```bash
logs/setup-completo.txt
```

---

# 🚀 Resultado

* ✔ Ambiente virtualizado funcional
* ✔ Rede NAT configurada
* ✔ Comunicação validada
* ✔ SSH ativo
* ✔ Ambiente pronto para DevOps

---

# 🔥 Próximos passos

* Docker
* Kubernetes (K3s)
* Terraform
* Simulação AWS local
* Hardening de segurança
