# 🛠️ Guia de Sobrevivência: Git & GitHub

Este documento contém referências rápidas para controle de versão com Git & GitHub.

## 🐙 Git & GitHub
O Git é um sistema distribuído que permite registrar e acompanhar mudanças em arquivos ao longo do tempo. 

O GitHub é uma plataforma de hospedagem em nuvem que armazena seus repositórios Git. 

### 1. Instalação

*Verifique se o Git já está instalado e sua versão atual.*
```
git --version
```

*Caso o git não esteja instalado, instale agora:*

**Downloads:** [Windows](https://git-scm.com/download/win) | [macOS](https://git-scm.com/download/mac) | [Linux](https://git-scm.com/download/linux)

### 2. Configuração Inicial

*Exiba as configurações atuais (nome, e-mail, etc).*
```
git config --list
```
*Caso o git não esteja configurado, configure agora:*
```
git config --global user.name "nome_usuario"
```
```
git config --global user.email "seu@email.com"
```

### 3. Fluxo de Trabalho Local
Versione seu projeto usando Git.

*Crie um novo repositório Git na pasta atual.*
```
git init
```
*Prepare um arquivo específico para o próximo commit.*
``` 
git add "nome_arquivo"
```
*Remova um arquivo específico da fila (desfaça o comando anterior).*
```
git rm --cached "nome_arquivo"
```
*Prepare TODOS os arquivos alterados da pasta atual para o próximo commit.*
```
git add .
```
*Grave as alterações preparadas com uma descrição do que foi feito.*
```
git commit -m "mensagem_commit"
```
*Mostre o estado atual: arquivos modificados, prontos ou não rastreados.*
```
git status
```

### 4. Histórico e Ramificações (Branches)
Explore a linha do tempo de modificações, crie e navegue pelas ramificações em seu projeto.

*Liste o histórico de todos os commits realizados.*
```
git log
```
*Mostre as diferenças detalhadas nos arquivos ainda não salvos.*
```
git diff
```
*Descarte mudanças locais e volte o arquivo ao estado do último commit.*
```
git restore "nome_arquivo"
```
*Liste as branches existentes no projeto.*
```
git branch
```
*Crie uma nova branch e mude para ela.*
```
git checkout -b "nome_branch"
```
*Troque para uma branch já existente.*
```
git checkout "nome_branch"
```
*Una o histórico e os arquivos da branch especificada à branch atual*
```
git merge "nome_branch"
```

### 5. Autenticação SSH (Opcional)
Evite a chatice de ter que se autenticar na conta do GitHub sempre que for dar um `git push`. Essa etapa deve ser realizada apenas em seu computador pessoal.

*Gere um par de chaves de segurança para seu PC.*
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
*Adicione a chave privada ao agente de autenticação.*
```
ssh-add ~/.ssh/id_ed25519
```
*Exiba a chave pública e a copie.*
```
cat ~/.ssh/id_ed25519
```
*Entre em [link](https://github.com/settings/keys), selecione "New SSH key" e cole a chave pública.*



### 6. Fluxo de Trabalho Remoto (GitHub)
Faça movimentações entre os ambientes remoto e local. 

*Crie uma cópia idêntica de um repositório remoto em seu ambiente local*
```
git clone https://link-do-repositorio.git
```
*Vincule seu repositório local a um servidor remoto.*
```
git remote add origin https://link-do-repositorio.git
```
*Envie seus commits locais para o ramo principal do servidor.*
```
git push origin main
```
*Traga as novidades do servidor e as mescle com seus arquivos locais.*
```
git pull origin main
```
*Busque atualizações do servidor sem alterar seus arquivos locais.*
```
git fetch
```

