---
title: 'Guia Geral sobre Redes'
description: >
  Um guia completo e prático para entender os principais protocolos de rede, seu funcionamento e como analisá-los no mundo real.
date: '2025-08-01T15:10:00-03:00'
draft: false
tags:
  - networking
  - protocols
  - tcpip
  - dns
categories:
  - docs
authors:
  - luk
cover:
  image: pattern.png
---

Se você quer trabalhar com segurança ofensiva, administração de sistemas, desenvolvimento web ou simplesmente entender como a internet realmente funciona, precisa dominar os **protocolos de rede**.

Neste guia, vamos explorar desde os analisadores de protocolo até DNS, passando por TCP/IP, Ethernet, ARP, IP, TCP, UDP e HTTP.

---

## 🔍 Analisadores de protocolo

Analisadores de protocolo permitem ver e estudar o tráfego real que circula na rede. Ferramentas como **Wireshark** e **tcpdump** mostram pacotes, cabeçalhos e dados em tempo real.

### Exemplos:
```bash
sudo tcpdump -i eth0
sudo tcpdump -n host 8.8.8.8
```

No **Wireshark**, você pode filtrar:
```
http
dns
tcp.port == 80
```

Essas ferramentas são essenciais para análise forense, troubleshooting e estudos de segurança.

---

## 🌐 Introdução ao TCP/IP

O **TCP/IP** é a base da comunicação na internet. Ele organiza a transmissão de dados em camadas:

1. **Aplicação** – protocolos como HTTP, FTP, DNS
2. **Transporte** – TCP, UDP
3. **Internet** – IP, ICMP, ARP
4. **Enlace** – Ethernet, Wi-Fi

Cada camada tem funções e protocolos específicos, garantindo que a comunicação seja padronizada.

---

## 📡 Protocolos de rede

Protocolos de rede são como idiomas padronizados que permitem que máquinas se entendam.  
Sem eles, cada fabricante teria seu próprio método de comunicação e nada funcionaria junto.

---

## 🖧 Protocolo Ethernet

O **Ethernet** opera na camada de enlace. Ele encapsula pacotes IP em quadros Ethernet, que contêm:

- **Endereço MAC de origem**
- **Endereço MAC de destino**
- **Tipo de protocolo encapsulado**

### Comando para ver MAC addresses:
```bash
ip link show
```

O Ethernet é usado principalmente em redes locais (LANs), cabos e switches.

---

## 🧠 Protocolo ARP

O **ARP (Address Resolution Protocol)** converte um endereço IP em endereço MAC.  
Quando um dispositivo quer se comunicar com outro na mesma rede, ele usa ARP para descobrir o MAC.

### Exibir tabela ARP:
```bash
arp -a
ip neigh
```

### Ataque comum:
- **ARP Spoofing** – falsifica respostas ARP para interceptar tráfego (Man-in-the-Middle).

---

## 📬 Protocolo IP

O **Internet Protocol** cuida do endereçamento e roteamento de pacotes.

- **IPv4**: endereços de 32 bits (ex: `192.168.0.1`)
- **IPv6**: endereços de 128 bits (ex: `2001:db8::1`)

### Tipos de endereços IPv4:
- **Públicos**: acessíveis pela internet
- **Privados**: usados em redes locais (`192.168.x.x`, `10.x.x.x`, `172.16.x.x` a `172.31.x.x`)

---

## 📦 Protocolo TCP

O **Transmission Control Protocol** é **orientado à conexão**.  
Ele garante entrega confiável dos dados, retransmitindo pacotes perdidos e ordenando-os corretamente.

Características:
- Handshake de 3 vias (SYN, SYN-ACK, ACK)
- Controle de fluxo
- Confirmação de recebimento (ACK)

### Ver conexões TCP ativas:
```bash
netstat -ant
ss -t
```

---

## ⚡ Protocolo UDP

O **User Datagram Protocol** é **sem conexão**.  
Não garante entrega nem ordem dos pacotes, mas é muito mais rápido.

Usado em:
- Streaming de vídeo
- Jogos online
- DNS
- VoIP

---

## 🌐 Protocolo HTTP

O **HyperText Transfer Protocol** é usado para comunicação entre navegadores e servidores web.

### Exemplo de requisição HTTP:
```
GET /index.html HTTP/1.1
Host: exemplo.com
```

Hoje usamos majoritariamente **HTTPS**, que adiciona criptografia via TLS.

---

## 🧭 DNS – Domain Name System

O **DNS** converte nomes como `google.com` em IPs como `142.250.69.206`.

### Fluxo básico:
1. Navegador pergunta ao **resolvedor local** (geralmente seu roteador).
2. Se não estiver no cache, consulta **servidores raiz**.
3. Os raiz indicam **servidores TLD** (`.com`, `.org`, `.br`).
4. Os TLD indicam os **servidores autoritativos** do domínio.
5. Resposta com o IP é enviada de volta ao cliente.

### Comandos úteis:
```bash
dig google.com
nslookup github.com
host openai.com
```

### Tipos de registros:
- **A**: aponta para IPv4
- **AAAA**: aponta para IPv6
- **MX**: servidor de e-mail
- **CNAME**: alias
- **TXT**: textos, SPF/DKIM

---

## 🔒 Segurança nos protocolos

Algumas vulnerabilidades comuns:
- **ARP Spoofing** – engana a tabela ARP.
- **DNS Spoofing/Poisoning** – responde com IP falso.
- **Sniffing** – captura pacotes TCP/HTTP sem criptografia.
- **Injeção** em protocolos mal configurados.

---

## 🧪 Prática recomendada

- Use o **Wireshark** para observar tráfego real.
- Capture um handshake TCP.
- Observe uma consulta DNS.
- Veja como pacotes HTTP aparecem sem criptografia.

Explorar protocolos na prática vai fixar o conhecimento muito mais do que apenas ler sobre eles.

---

Entender protocolos é como falar a língua da internet. É o que diferencia alguém que usa a rede de alguém que **domina** a rede.
