---
title: 'Usuários e Permissões no Linux'
description: >
  Entenda como funciona a criação de usuários, grupos, permissões de leitura, escrita e execução no sistema Linux.
date: '2025-08-01T14:30:00-03:00'
draft: false
tags:
  - linux
  - permissions
categories:
  - docs
authors:
  - luk
cover:
  image: pattern.png
---

Saber gerenciar usuários e permissões no Linux é essencial para manter o sistema seguro e organizado, especialmente em ambientes multiusuário ou servidores.

Vamos explorar os comandos e conceitos fundamentais para lidar com contas, grupos e permissões no Linux.

---

## 👥 Gerenciamento de Usuários

### `adduser` / `useradd` - Criar usuários

```bash
adduser nome_usuario        # cria usuário com assistente interativo
useradd nome_usuario        # método mais direto
```

### `passwd` - Definir ou alterar senha

```bash
passwd nome_usuario         # define ou altera a senha do usuário
```

### `deluser` / `userdel` - Remover usuários

```bash
deluser nome_usuario
userdel nome_usuario
userdel -r nome_usuario     # remove também o diretório home
```

---

## 👪 Gerenciamento de Grupos

### `addgroup` / `groupadd` - Criar grupo

```bash
addgroup grupo
groupadd grupo
```

### `usermod` - Adicionar usuário a grupo

```bash
usermod -aG grupo nome_usuario    # adiciona sem remover dos grupos anteriores
```

### `groups` - Ver grupos de um usuário

```bash
groups                           # mostra os grupos do usuário atual
groups nome_usuario              # mostra grupos de outro usuário
```

---

## 🔐 Permissões de Arquivos

No Linux, arquivos e diretórios têm permissões definidas por:

- **Usuário (owner)**
- **Grupo**
- **Outros (others)**

### Ver permissões com `ls -l`

```bash
ls -l arquivo.txt
```

Saída exemplo:

```
-rw-r--r-- 1 luk users 1024 ago 1 08:00 arquivo.txt
```

Significado:

- `rw-` = dono pode ler e escrever
- `r--` = grupo pode apenas ler
- `r--` = outros podem apenas ler

---

## 🛠 Alterar permissões

### `chmod` - Mudar permissões

```bash
chmod 755 script.sh        # rwxr-xr-x
chmod u+x arquivo.sh       # adiciona permissão de execução para o dono
chmod -R 644 *.txt         # aplica recursivamente
```

Tabela rápida:
- `r` = 4 (read)
- `w` = 2 (write)
- `x` = 1 (execute)

---

## 👤 Alterar dono e grupo

### `chown` - Mudar o dono do arquivo

```bash
chown usuario arquivo.txt
chown usuario:grupo arquivo.txt
```

### `chgrp` - Mudar apenas o grupo

```bash
chgrp grupo arquivo.txt
```

---

## 🔒 Permissões especiais (avançado)

### Sticky Bit

Impede que usuários deletem arquivos de outros em diretórios compartilhados (como `/tmp`):

```bash
chmod +t /diretorio
```

### Setuid e Setgid

Permite que um executável rode com permissões do dono ou grupo:

```bash
chmod u+s binario     # setuid
chmod g+s pasta       # setgid
```

---

## 🔍 Ver UID, GID, permissões atuais

```bash
id                      # mostra UID, GID e grupos
stat arquivo.txt        # detalhes completos do arquivo
```

---

Gerenciar usuários e permissões é um pilar da administração de sistemas Linux e também da segurança ofensiva: um atacante precisa saber como escalar privilégios, e um defensor precisa saber como impedir isso.

---