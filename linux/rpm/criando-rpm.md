---
title: Criando Pacotes RPM
---

# Criando Pacotes RPM

## Criando o usuário

Para criar os pacotes RPM, é necessário criar um usuário que não seja administrador do sistema (non-root user). O diretório home do usuário será usado como base para armazenar os scripts, fontes e pacotes RPM criados.

**1.** Criando o usuário não administrador. Pode-ser escolher qualquer nome para o usuário, porém, neste exemplo, será usado o nome **"builder"** (construtor) que é um nome comum para os usuários que criam pacotes.

```shell
[user@myhostname ~]$ sudo useradd -c "Usuário para criar pacotes RPM" -m builder
```

**2.** Verificando se o usuário foi criado no no arquivo **/etc/passwd**.

```shell
[user@myhostname ~]$ cat /etc/passwd | grep builder
builder:x:1001:1001:Usuário para criar pacotes RPM:/home/builder:/bin/bash
```

**3.** Verificando os grupos que o usuário "builder" pertence.

```shell
[user@myhostname ~]$ id builder
uid=1001(builder) gid=1001(builder) groups=1001(builder)
```



## Criando a primeira estrutura de pacotes

**1.** Instalando os pacotes e dependências necessárias para montar uma estrutura de pacotes
```shell
[user@myhostname ~]$ sudo dnf install -y rpmdevtools rpmlint tree git
```

**2.** Trocar usuário para o "**builder**"

```shell
[user@myhostname ~]$ sudo su - builder
```

**3.** Criar a estrutura de diretórios para criar um novo pacote. Será criado um diretório chamado **rpmbuild** com subdiretórios

```shell
[builder@myhostname ~]$ rpmdev-setuptree
[builder@myhostname ~]$ tree $HOME
/home/builder
└── rpmbuild
    ├── BUILD
    ├── RPMS
    ├── SOURCES
    ├── SPECS
    └── SRPMS

6 directories, 0 files
```



```shell
[builder@myhostname ~]$ cd rpmbuild/SPECS

[builder@myhostname SPECS]$ rpmdev-newspec hello
hello.spec created; type minimal, rpm version >= 4.14.

[builder@myhostname SPECS]$ tree $HOME
/home/builder
└── rpmbuild
    ├── BUILD
    ├── RPMS
    ├── SOURCES
    ├── SPECS
    │   └── hello.spec
    └── SRPMS

6 directories, 1 file
```

