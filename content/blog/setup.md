---
title: "Setup do Curso de C no Windows com WSL"
date: 2024-05-13T21:15:08-03:00
draft: false
tags:
    - C
    - UBL
    - Desenvolvimento
    - Ferramentas
---

**Contexto:**
> Na [UBL](https://ulivre.dev/) (Universidade Brasileira Livre), estamos organizando um grupo de estudos de C. Selecionamos alguns materiais, como o [Programação Moderna em C](https://youtube.com/playlist?list=PLIfZMtpPYFP5qaS2RFQxcNVkmJLGQwyKE&si=XPRRx0g_8hASdQeN) e o [C para Seres Humanos](https://plankiton.github.io/CParaSeresHumanos/), por serem recursos livres, gratuitos e em português sobre a linguagem C.

Como atualmente estou usando o Windows como meu sistema operacional principal (devido a algumas aplicações específicas), resolvi criar este guia para mostrar como configurei meu ambiente de desenvolvimento.

## Atualizando o PowerShell e os Programas do Windows

Antes de começarmos, é importante garantir que o PowerShell e todos os outros programas do Windows estejam atualizados. Isso garantirá que você tenha as últimas funcionalidades e correções de segurança.

Abra o PowerShell como administrador e execute os seguintes comandos:

```powershell
winget upgrade --all
```
```powershell
winget install --id Microsoft.Powershell --source winget
```

O primeiro comando atualiza todos os programas instalados, enquanto o segundo reinstala o PowerShell para a versão mais recente disponível.

## Instalando o WSL 2

Com o sistema atualizado, podemos prosseguir com a instalação do WSL 2. O WSL permite que você execute um ambiente Linux diretamente no Windows sem a necessidade de uma máquina virtual.

Digite o seguinte comando no PowerShell:

```powershell
wsl --install
```

Após a execução, será necessário reiniciar o computador. Ao reiniciar, o Windows solicitará que você crie um usuário e senha para o Ubuntu, que será instalado por padrão.

Quando o Ubuntu estiver instalado, abra o terminal do Ubuntu e atualize os pacotes:

```bash
sudo apt update && sudo apt upgrade -y
```

## Configurando o Terminal para Abrir o WSL por Padrão

Para uma melhor experiência visual e funcional, vamos personalizar o terminal com uma fonte mais agradável e um esquema de cores diferenciado.

1. **Instalando a Fonte JetBrains Mono NerdFont:**
   - No Windows, baixe a fonte JetBrains Mono NerdFont do site [Nerd Fonts](https://www.nerdfonts.com/font-downloads).
   - Descompacte o arquivo baixado e instale todas as fontes presentes na pasta `.ttf`.

2. **Definindo o Perfil Padrão para Ubuntu:**
   - No Windows Terminal, clique na seta para baixo ao lado do título e selecione 'Opções'.
   - Em 'Perfil Padrão', escolha 'Ubuntu'.

3. **Aplicando o Esquema de Cores Dracula:**
   - Abra o Windows Terminal e clique na seta para baixo ˅ na barra de menu.
   - Selecione 'Configurações' ou use `Ctrl + ,` para abrir diretamente.
   - No arquivo `settings.json`, encontre a seção 'schemes' e adicione o conteúdo do `dracula.json`.

4. **Personalizando a Aparência do Ubuntu no Terminal:**
   - Na barra lateral, selecione 'Ubuntu' e depois 'Aparência'.
   - Escolha o esquema de cores 'Dracula'.
   - Em 'Fonte', marque 'Mostrar todas' e selecione 'JetBrains Mono NerdFont'.

5. **Salve as alterações.**

## Instalando o ZSH

O ZSH é um shell poderoso e fácil de personalizar. Para instalá-lo, execute:

```bash
sudo apt install zsh -y
```
```bash
chsh -s $(which zsh)
```

## Instalando o Powerlevel10k

Powerlevel10k é um tema rápido e bonito para o ZSH. Instale-o com:

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
```
```bash
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

Siga as instruções de configuração que aparecerão após a instalação.

## Instalando o zsh-autosuggestions

Para obter sugestões automáticas enquanto digita no terminal, instale o zsh-autosuggestions:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
```
```bash
echo 'source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh' >>~/.zshrc
```

## Instalando o Pacstall

Pacstall é um gerenciador de pacotes que facilita a instalação de software. Para instalá-lo, execute:

```bash
sudo bash -c "$(curl -fsSL https://pacstall.dev/q/install || wget -q https://pacstall.dev/q/install -O -)"
```

Confirme as instalações conforme solicitado. Isso também instalará a toolchain do GCC para C.

Adicione o seguinte ao seu `.zshrc` para habilitar a conclusão automática para o Pacstall:

```bash
echo '\nautoload bashcompinit \nbashcompinit' >>~/.zshrc
```
```bash
echo 'source /usr/share/bash-completion/completions/pacstall' >>~/.zshrc
```

## Instalando e Configurando o (Neo)Vim

O (Neo)Vim é um editor de texto avançado. Para instalar e configurar:

```bash
pacstall -I neovim
```

Siga as instruções de configuração recomendadas por especialistas, como as do Akita.

## Instalando o Docker

Para instalar o Docker:

- Baixe e instale o Docker do site oficial.
- Vá em 'Configurações' > 'Recursos' > 'Integração WSL' e ative o Ubuntu.
- Aceite os termos de uso.

Teste sua instalação com:

```bash
docker run -d -p 80:80 docker/getting-started
```

Se tudo estiver correto, acesse [http://localhost](http://localhost) e você verá a página inicial do Docker.