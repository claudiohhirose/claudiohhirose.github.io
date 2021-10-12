---
title: Criando Pacotes RPM
---

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

