---
title: 'Principais comandos Linux'
description: >
    Comandos essenciais de terminal Linux para quem quer dominar a arte do Shell.
date: '2025-08-01T08:30:00-03:00'
draft: false
tags:
    - linux
    - shell
    - terminal
categories:
    - docs
authors:
    - luk
cover:
    image: pattern.png
---

O terminal é uma das ferramentas mais poderosas que existem no Linux. Se você está começando sua jornada como hacker, sysadmin ou desenvolvedor, entender os comandos básicos do shell é obrigatório.

Neste post, vamos explorar os principais comandos e como usá-los na prática.

---

## 📁 Navegação entre diretórios

### `ls` - Lista arquivos e diretórios

```bash
ls              # lista arquivos
ls -l           # exibe detalhes (long format)
ls -a           # mostra arquivos ocultos
ls -lh          # tamanhos legíveis
ls -la          # detalhes + ocultos
```

### `cd` - Muda de diretório

```bash
cd /caminho/para/pasta
cd ..           # volta um nível
cd ~            # vai para o diretório home
```

---

## 🗂 Copiar, mover e remover arquivos

### `cp` - Copia arquivos

```bash
cp origem.txt destino/
cp -r pasta/ /destino/     # cópia recursiva de pastas
```

### `mv` - Move ou renomeia arquivos

```bash
mv arquivo.txt /destino/
mv antigo.txt novo.txt
```

### `rm` - Remove arquivos e pastas

```bash
rm arquivo.txt
rm -r pasta/               # remove pasta recursivamente
rm -rf /                   # ⚠️ apaga tudo, use com extremo cuidado
```

---

## 📊 Espaço em disco

### `df` - Ver uso de disco

```bash
df -h                      # mostra espaço em disco em formato legível
```

### `du` - Tamanho de arquivos e diretórios

```bash
du -sh *                   # mostra tamanho de tudo na pasta atual
```

---

## 📥 Download de arquivos

### `wget` - Faz download de um arquivo pela URL

```bash
wget https://site.com/arquivo.zip
```

---

## 🔍 Busca de conteúdo

### `grep` - Busca por padrões em arquivos

```bash
grep "texto" arquivo.txt
grep -i "palavra" arquivo.txt     # ignora maiúsculas/minúsculas
grep -r "palavra" /caminho        # busca recursiva
grep -n "erro" log.txt            # mostra número da linha
grep -v "string" arquivo.txt      # mostra linhas que NÃO contêm a string
```

---

## 🧪 Expressões Regulares com `grep`

```bash
grep "^root" /etc/passwd          # começa com 'root'
grep "[0-9]" arquivo.txt          # linhas com números
grep -E "erro|fail" log.txt       # erro OU fail
```

---

## ✂️ Manipulação de colunas e caracteres

### `cut` - Recorta partes de uma linha

```bash
cut -d ':' -f1 /etc/passwd        # mostra primeira coluna, separada por ':'
cut -c 1-5 arquivo.txt            # mostra caracteres da coluna 1 à 5
```

---

## 📢 Exibir mensagens ou variáveis

### `echo` - Mostra no terminal

```bash
echo "Olá mundo!"
echo $USER
echo "Usuário: $USER, Diretório: $PWD"
```

### Redirecionamento com `>` e `>>`

```bash
echo "linha nova" > arquivo.txt     # sobrescreve o arquivo
echo "outra linha" >> arquivo.txt   # adiciona ao final
```

---

## 🧠 Dica de ouro: combine comandos

Você pode usar pipes (`|`) para conectar comandos entre si:

```bash
cat arquivo.txt | grep "erro" | cut -d ' ' -f2
```

---

Dominar e aprender esses comandos é um passo essencial no caminho de qualquer hacker, entusiasta de Linux e até mesmo desenvolvedor. Continue praticando, criando seus próprios scripts e explorando novas opções!