# 🚀 KVM + Ubuntu Server 24.04 Lab


![OS](https://img.shields.io/badge/OS-Windows-blue?logo=windows)
![Virtualization](https://img.shields.io/badge/Virtualization-WSL-red)
![Linux](https://img.shields.io/badge/OS-Linux-blue?logo=linux)
![KVM](https://img.shields.io/badge/Virtualization-KVM-red)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04_LTS-orange?logo=ubuntu)
![Status](https://img.shields.io/badge/status-active-success)
![Security](https://img.shields.io/badge/security-best_practices-green)

---

Projeto prático de virtualização utilizando **KVM/QEMU** no Linux (Pop!_OS), com criação e configuração de uma VM Ubuntu Server 24.04 LTS e acesso remoto via SSH.

---

## 🖥️ Arquitetura do Ambiente

![Diagrama](docs/diagrama_kvm_0.png)

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

## 🔧 1. Instalação completa do ambiente KVM (HOST)

## Atualização do sistema

```bash
sudo apt update && sudo apt upgrade -y
```

---
## Instalação dos pacotes de virtualização

```bash
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager -y

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

## 🌐 2. Configuração da rede virtual (NAT)

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
192.168.X.X/X
```

---

## 🖥️ 3. Criação da Máquina Virtual

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

## 🧪 4. Testes de conectividade (HOST)

```bash
ip a
ping 192.168.X.X
```

---

## 🔐 5. Acesso remoto via SSH

```bash
ssh user@192.168.X.X
```

---

## 🖥️ 6. Configuração do Ubuntu Server (VM)

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

## ⚠️ Problemas e correções

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
ssh user@192.168.X.X/X
```

### Correto:

```bash
ssh user@192.168.X.X
```

---

## ❌ Sem internet na VM

### Verificar:

```bash
ip a
ping 192.168.122.1
```

---

## 📸 Evidências

![Host](docs/ip-host.png)
![Ping](docs/ping-vm.png)
![SSH](docs/ssh-login.png)

---

## 📂 Logs

```bash
logs/setup-completo.txt
```

---

## 🚀 Resultado

* ✔ Ambiente virtualizado funcional
* ✔ Rede NAT configurada
* ✔ Comunicação validada
* ✔ SSH ativo
* ✔ Ambiente pronto para DevOps

---
## 🌐 Exposição externa com Cloudflare Tunnel

### 🖥️ Sessão tmux

![tmux](docs/tmux.png)

### 🌐 Servidor local

![server](docs/server.png)

### 🔐 Tunnel ativo

![tunnel](docs/tunnel.png)

### 🌍 Acesso externo

![acesso](docs/acesso-publico.png)

Exemplo de URL gerada:

https://justice-conflict-properties-geological.trycloudflare.com/

> URL dinâmica (modo quick tunnel)

A exposição externa foi realizada via Cloudflare Tunnel (modo quick tunnel), com HTTPS automático. Em ambiente de produção, recomenda-se uso de domínio próprio para URL fixa.

- Comunicação segura via HTTPS (Cloudflare)
- Sem necessidade de abertura de portas no roteador (NAT bypass)




## 🪟 Execução em Windows (WSL2)

![OS](https://img.shields.io/badge/OS-Windows-blue?logo=windows)
![Virtualization](https://img.shields.io/badge/Virtualization-WSL-red)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04_LTS-orange?logo=ubuntu)
![Status](https://img.shields.io/badge/status-active-success)
![Security](https://img.shields.io/badge/security-best_practices-green)

Este projeto também pode ser executado em ambiente Windows utilizando o **WSL2 (Windows Subsystem for Linux)**, que fornece um kernel Linux real integrado ao sistema.

## 🖥️ Arquitetura do Ambiente

![Diagrama](docs/diagrama_wsl_1.png)

---

### 📌 Pré-requisitos

* Windows 10 (2004+) ou Windows 11
* Virtualização habilitada na BIOS/UEFI (Intel VT-x ou AMD-V)

---

### ⚙️ Configuração do Windows

#### ✔️ Recursos que devem estar habilitados

No PowerShell (Administrador):

```bash
wsl --install
```

Esse comando habilita automaticamente:

* Plataforma de Máquina Virtual
* Subsistema do Windows para Linux
* Hypervisor (necessário para WSL2)

---

### 🔍 Verificar status

```bash
wsl --status
```

---

### 🔄 Definir WSL2 como padrão

```bash
wsl --set-default-version 2
```

---

### 🐧 Instalar Ubuntu 24.04 LTS

```bash
wsl --install -d Ubuntu-24.04
```

Após instalar:

* criar usuário
* definir senha

---

### 🚀 Acessar o Linux

```bash
wsl
```

ou:

```bash
wsl -d Ubuntu-24.04
```

---

### 📡 Rede no WSL

O WSL utiliza NAT interno, semelhante ao KVM:

* acesso à internet: automático
* acesso externo: requer túnel (ex: Cloudflare Tunnel)

---

### 🔐 Acesso SSH no WSL

Instalar:

```bash
sudo apt update && sudo apt install openssh-server -y
```

Iniciar:

```bash
sudo service ssh start
```

---

### ⚠️ Hyper-V e Virtualização

* O WSL2 **usa o hypervisor do Windows (Hyper-V)** internamente
* Não é necessário desativar manualmente
* Deve estar **habilitado automaticamente**

✔ recomendado: manter ativado
❌ não usar modo "off"

---

### 🚫 Limitação importante

O WSL2 **não suporta KVM/libvirt diretamente**, pois já utiliza o hypervisor do Windows.

👉 Portanto:

* KVM → usar Linux (Pop!_OS, Ubuntu)
* WSL → ambiente alternativo para desenvolvimento

---

## 💻 Integração com VS Code (WSL)

O VS Code permite desenvolvimento direto dentro do WSL com ambiente Linux completo.

---

### 🔧 Instalar extensão

No VS Code, instale:

👉 **Remote - WSL**

---

### 🚀 Abrir projeto no WSL

No terminal do WSL:

```bash
code .
```

---

### 📂 Alternativa pelo VS Code

1. Abrir VS Code
2. `Ctrl + Shift + P`
3. Digitar:

```bash
Remote-WSL: Open Folder in WSL
```

---

### 📌 Como funciona

* VS Code roda no Windows
* Código executa dentro do Linux (WSL)
* Terminal integrado usa Ubuntu
* Permite usar ferramentas Linux nativas (apt, ssh, node, etc.)

---

### 🔥 Vantagens

✔ Ambiente Linux real no Windows
✔ Integração direta com terminal
✔ Compatível com Git e SSH
✔ Ideal para desenvolvimento full stack

---

### ⚠️ Observação

Para projetos com virtualização avançada (KVM/libvirt), utilize Linux nativo.

---

### 🧠 Resumo

| Ambiente       | Uso recomendado     |
| -------------- | ------------------- |
| WSL2 + VS Code | Desenvolvimento     |
| Linux nativo   | Virtualização (KVM) |

---

### 🎯 Uso no projeto

Neste projeto, o WSL pode ser utilizado para:

* executar comandos Linux
* gerenciar arquivos
* usar SSH
* integrar com GitHub

Enquanto a virtualização KVM é executada no host Linux (Pop!_OS).
