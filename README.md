# infraestrutura-servidores-redes
"Trabalho sobre infraestrutura de servidores () 
### Trabalho da disciplina [cyber segurança]  
**Aluno:** Dieudonne kadima badibanga
**Objetivo:** Descreva as principais configuraçãos windos e debiam 

Resumo Detalhado: Instalação e Configuração de Sistemas de Rede (Debian Linux e Windows Server)
Este guia cobre os passos essenciais para instalar e configurar Debian Linux e Windows Server em um ambiente de rede, incluindo serviços básicos como DNS, DHCP e Active Directory.

1. Instalação e Configuração do Debian Linux
O que é o Debian?
Sistema operacional Linux gratuito, estável e amplamente usado em servidores.

Ideal para serviços como DNS, DHCP, Wazuh (monitoramento), Ansible (automação).

Passos para Instalação
Baixar a ISO

Acesse debian.org/download e baixe a ISO "netinst" (instalação mínima via internet).

Criar Máquina Virtual (VM) ou Instalar em Hardware

Use VirtualBox, VMware ou Hyper-V para criar uma VM.

Configure:

2+ GB de RAM

20+ GB de armazenamento

Rede em modo Bridge/NAT

Instalação Básica

Inicie a instalação e selecione:

Idioma: Português (Brasil)

Teclado: ABNT2

Hostname: servidor-debian

Domínio: (deixe em branco ou use local)

Particionamento: Guided - usar todo o disco

Usuário: Crie um usuário admin (ex: admin)

Configuração de Rede

Verifique o IP com:

bash
ip a
Configure IP estático (edite /etc/network/interfaces):

bash
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
Reinicie a rede:

bash
systemctl restart networking
Atualizar o Sistema

bash
sudo apt update && sudo apt upgrade -y
2. Instalação e Configuração do Windows Server
O que é o Windows Server?
Sistema da Microsoft para servidores corporativos.

Usado para Active Directory (AD), DNS, DHCP, Gerenciamento de Usuários.

Passos para Instalação
Baixar a ISO

Obtenha a ISO do Windows Server 2022 via Microsoft Evaluation Center.

Criar Máquina Virtual (VM) ou Instalar em Hardware

Requisitos mínimos:

2 vCPUs, 4+ GB RAM, 60 GB HDD

Rede em modo Bridge

Instalação Básica

Inicie a instalação e selecione:

Edição: Windows Server 2022 Standard (Desktop Experience)

Particionamento: Use todo o disco

Senha de Administrador: Crie uma senha forte

Configuração de Rede

Abra "Server Manager" > "Local Server" > "Ethernet"

Defina um IP estático:

IPv4: 192.168.1.200

Máscara: 255.255.255.0

Gateway: 192.168.1.1

DNS: 8.8.8.8 (ou o IP do seu servidor DNS)

Ativar e Renomear o Servidor

Abra PowerShell e execute:

powershell
Rename-Computer -NewName "SRV-WIN-01" -Restart
3. Configuração de Serviços Básicos
No Debian (Linux)
Instalar e Configurar DNS (BIND9)

bash
sudo apt install bind9 -y
Editar /etc/bind/named.conf.local para adicionar zonas.

Instalar e Configurar DHCP (ISC-DHCP-Server)

bash
sudo apt install isc-dhcp-server -y
Configurar /etc/dhcp/dhcpd.conf com faixas de IP.

No Windows Server
Instalar Active Directory (AD) e DNS

No Server Manager, clique em "Add Roles and Features".

Selecione "Active Directory Domain Services" e "DNS Server".

Promova o servidor a Controlador de Domínio (usando dcpromo ou via assistente).

Configurar DHCP

Adicione a função DHCP Server.

Crie um escopo de IP (ex: 192.168.1.50 a 192.168.1.150).

4. Comparação: Debian vs. Windows Server
Tarefa	Debian Linux	Windows Server
Instalação	Terminal (texto) ou GUI mínima	Assistente gráfico
Custo	Gratuito (open-source)	Pago (licenciamento)
Serviços	DNS, DHCP, Wazuh, Ansible (via CLI)	AD, DNS, DHCP (GUI fácil)
Usuários	Gerenciamento manual (usuários Linux)	Active Directory (centralizado)
Segurança	Firewall (iptables/nftables)	Firewall do Windows + Defender
Próximos Passos
Testar a rede entre Debian e Windows (ping).

Configurar mais serviços (Wazuh, Ansible, PfSense).

Automatizar tarefas com scripts Ansible.

Precisa de detalhes sobre algum serviço específico? Posso ajudar com tutoriais mais aprofundados! 🚀

unifique para eu copiar
Guia Unificado: Instalação e Configuração de Debian Linux e Windows Server
1. Debian Linux
Instalação
Baixar ISO

Acesse debian.org/download e baixe a versão "netinst".

Configurar VM/Hardware

Requisitos: 2 GB RAM, 20 GB armazenamento, rede em modo Bridge.

Use VirtualBox/VMware ou instale diretamente no hardware.

Processo de Instalação

Selecione idioma (Português-BR), teclado (ABNT2).

Defina:

Hostname: servidor-debian

Domínio: (opcional)

Particionamento: Guided - usar disco inteiro

Usuário: Crie um (ex: admin).

Configuração de Rede

Edite /etc/network/interfaces:

bash
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
Reinicie:

bash
systemctl restart networking
Atualizar Sistema

bash
sudo apt update && sudo apt upgrade -y
2. Windows Server
Instalação
Baixar ISO

Obtenha a ISO do Windows Server 2022 em Microsoft Evaluation Center.

Configurar VM/Hardware

Requisitos: 4 GB RAM, 60 GB armazenamento, rede Bridge.

Processo de Instalação

Selecione:

Edição: Windows Server 2022 Standard (Desktop Experience)

Particionamento: Use disco completo.

Senha de Admin: Crie uma senha forte.

Configuração de Rede

Server Manager > Local Server > Ethernet

IP estático: 192.168.1.200

Máscara: 255.255.255.0

Gateway: 192.168.1.1

DNS: 8.8.8.8

Renomear Servidor

No PowerShell:

powershell
Rename-Computer -NewName "SRV-WIN-01" -Restart
3. Configuração de Serviços
Debian Linux
DNS (BIND9):

bash
sudo apt install bind9 -y
Configure zonas em /etc/bind/named.conf.local.

DHCP (ISC-DHCP-Server):

bash
sudo apt install isc-dhcp-server -y
Edite /etc/dhcp/dhcpd.conf para definir faixas de IP.

Windows Server
Active Directory (AD) e DNS:

Server Manager > Add Roles and Features.

Selecione AD Domain Services e DNS Server.

Promova o servidor a Domain Controller (via assistente).

DHCP:

Adicione a função DHCP Server.

Crie um escopo (ex: 192.168.1.50-150).

4. Comparação Rápida
Tarefa	Debian Linux	Windows Server
Instalação	Terminal/GUI mínima	Assistente gráfico
Custo	Gratuito	Pago (licença)
Serviços	DNS, DHCP (CLI)	AD, DNS, DHCP (GUI)
Segurança	iptables/nftables	Windows Defender + Firewall
Próximos Passos
Testar comunicação (ping entre servidores).

Implementar Wazuh (monitoramento) ou Ansible (automação).

Documentar tudo no GitHub com pastas organizadas.
