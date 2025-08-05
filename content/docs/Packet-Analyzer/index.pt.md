---
title: "Análise Suprema de Pacotes: Do tcpdump ao Wireshark"
description: >
  Domine a análise de pacotes com este guia completo — aprenda tudo sobre headers, payloads, tcpdump, Wireshark e protocolos criptografados.
date: 2025-08-05T16:00:00-03:00
draft: false
tags:
  - networking
  - tcpdump
  - wireshark
  - packet-analysis
  - protocolos
categories:
  - docs
authors:
  - luk
cover:
  image: pattern.png
---

# 🧠 Análise Suprema de Pacotes: Do tcpdump ao Wireshark

No nosso **Guia Geral sobre Redes**, exploramos os fundamentos dos protocolos. Agora, chegou a hora de ir mais fundo. Vamos realmente **observar, ler e entender os pacotes** que trafegam pela sua rede.

Este guia é o mais completo que você vai encontrar: **tcpdump, Wireshark, headers, payloads, criptografia, protocolos, práticas recomendadas — tudo explicado em português claro.**

---

## 📦 Anatomia de um Pacote de Rede

Um pacote é como uma carta:

- **Cabeçalho (Header)**: contém endereços, controle e metadados.
- **Payload (Carga útil)**: o conteúdo — mensagem, página, arquivo.

Camadas do Modelo OSI envolvidas:

- **Camada 2 (Enlace)**: MACs, Ethernet.
- **Camada 3 (Rede)**: IPs, TTL, fragmentação.
- **Camada 4 (Transporte)**: TCP/UDP, portas, flags.
- **Camada 7 (Aplicação)**: HTTP, DNS, etc.

---

## ⚙️ Ferramentas de Captura e Análise

### 1. `tcpdump` (linha de comando)
```bash
sudo tcpdump -i eth0 -n -vv
```

- `-i eth0`: Interface a ser monitorada.
- `-n`: Não resolver nomes (mais rápido).
- `-vv`: Verbosidade (veja mais detalhes).

### 2. Wireshark (interface gráfica)

- Permite filtros visuais, reconstrução de fluxos, estatísticas de protocolo.
- Ideal para quem prefere visual e quer "ver" o tráfego acontecendo.

---

## 🧾 Lendo Saídas do tcpdump

Exemplo:
```bash
15:57:09.259316 IP 192.168.0.2.60262 > 142.250.184.206.https: Flags [.], ack 123456789, win 501, length 0
```

Quebrando:

- **Timestamp**: 15:57:09.259316
- **Protocolo**: IP (IPv4)
- **Origem**: 192.168.0.2:60262
- **Destino**: 142.250.184.206:443 (https)
- **Flags**: ACK (`.`)
- **ack**: Número de confirmação
- **win**: Tamanho da janela de recepção
- **length**: Tamanho do payload (0 = apenas controle)

---

## 🏷️ Flags TCP mais comuns

- `[S]`: SYN – início de conexão
- `[.]`: ACK – confirmação
- `[P]`: PSH – envio imediato
- `[F]`: FIN – encerramento de conexão
- `[R]`: RST – reset
- `[U]`: URG – dado urgente

---

## 🌐 Exemplo: Pacote DNS

```bash
15:57:09.319786 IP 192.168.0.2.45821 > dns.google.domain: 37311+ PTR? 206.184.250.142.in-addr.arpa. (44)
```

- **PTR?**: Consulta reversa
- **37311+**: ID da requisição DNS com recursão habilitada
- **dns.google.domain**: servidor DNS na porta 53
- **(44)**: tamanho total da consulta

---

## 🔐 O Que Dá Pra Ver?

### Sem Criptografia (HTTP, FTP):
- Cabeçalhos e payloads legíveis
- Senhas, comandos, páginas

### Com Criptografia (HTTPS, SSH):
- Só cabeçalhos visíveis
- Payload criptografado (indecifrável)

**DICA:** Você ainda pode ver:
- IPs e portas
- Volume de dados
- Timing e padrões

---

## 🕵️‍♂️ Dicas de Filtros no tcpdump

- Capturar apenas tráfego HTTP:
  ```bash
  tcpdump -i eth0 port 80
  ```
- Capturar só tráfego de um IP:
  ```bash
  tcpdump host 192.168.0.5
  ```
- Ver apenas pacotes DNS:
  ```bash
  tcpdump port 53
  ```

---

## 🎨 Wireshark: Dicas Visuais

- Use **filtros de exibição**:
  - `http`, `dns`, `tcp.port == 443`
- Clique com botão direito em um pacote → **Follow → TCP Stream**
- Visualize handshakes, sessões completas, SSL, TLS
- **Statistics → Protocol Hierarchy**: veja tudo que rolou

---

## 🧪 Prática: Exercícios Reais

1. Capture um handshake TCP completo
2. Acesse um site HTTP e veja conteúdo no Wireshark
3. Observe um DNS em tempo real
4. Use filtros para separar tráfego por IP ou protocolo
5. Compare pacotes HTTP e HTTPS

---

## 🧰 Protocolos Populares Observáveis

- **HTTP**: Totalmente visível (se não for HTTPS)
- **HTTPS**: Apenas cabeçalhos (criptografado)
- **DNS**: Visível, exceto DNS-over-HTTPS
- **SSH**: Apenas IPs/portas visíveis
- **SMTP**: Muitas vezes em texto claro (sem TLS)
- **FTP**: Texto claro, vulnerável

---

## 🧠 Conclusão

Analisar pacotes é **ler a linguagem da internet**. Ferramentas como `tcpdump` e Wireshark são essenciais pra qualquer pessoa que trabalha com redes, segurança ou deseja entender o que acontece nos bastidores.

Com esse guia você está pronto pra:
- Ler pacotes com fluência
- Diferenciar tráfego seguro de inseguro
- Identificar problemas de rede
- Fazer auditoria de segurança básica

Agora, é hora de **observar o tráfego real**, filtrar, interpretar e se tornar um verdadeiro analista de rede.

---

**🚀 Boa prática!**
