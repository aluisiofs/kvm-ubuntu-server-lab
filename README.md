# 🚀 KVM + Ubuntu Server 24.04 Lab

Projeto prático de virtualização utilizando KVM no Linux (Pop!_OS) com criação de máquina virtual Ubuntu Server 24.04.4 LTS e acesso remoto via SSH.

---

## 🖥️ Ambiente

* Host: Pop!_OS Linux
* Virtualização: KVM / QEMU / libvirt
* VM: Ubuntu Server 24.04.4 LTS
* Rede: NAT (virbr0)
* Acesso: SSH

---

## 🔧 Etapas realizadas

### ✔ Configuração do ambiente KVM

* Instalação do KVM e ferramentas
* Ativação do serviço libvirt

### ✔ Configuração de rede

* Interface NAT: 192.168.X.X
* Bridge: virbr0

### ✔ Criação da VM

* ISO Ubuntu Server 24.04
* Configuração de CPU, RAM e disco
* Interface de rede virtio

### ✔ Testes de conectividade

* Ping entre host e VM
* Validação de IP

### ✔ Acesso remoto via SSH

* Configuração do OpenSSH Server
* Conexão via terminal do host

---

## 🧪 Testes realizados

* ✔ ping 192.168.X.X
* ✔ ssh aluisio@192.168.122.X
* ✔ ip a

---

## ⚠️ Problemas encontrados e solução

### ❌ Erro SSH

Comando incorreto:

ssh aluisio@192.168.122.X/X

Erro:
Could not resolve hostname

### ✅ Solução

Uso correto:

ssh aluisio@192.168.X.X

---

## 📂 Logs

Ver detalhes completos em:

logs/setup-kvm.txt

---

## 🚀 Próximos passos

* Configurar SSH sem senha
