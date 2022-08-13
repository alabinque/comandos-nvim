# Instalação

## Instalar o elixir

### Instalar o asdf
1. Instalar as dependências.
  - No linux: `$ sudo apt install curl git`
  - No mac: `$ brew install coreutils curl git` 
2. Clone o source do asdf. 
  - `$ git clone https://github.com/asdf-vm/asdf.git ~/.asdf`
3. Adicione a seguinte linha do seu `~/.bashrc` ou `~/.zshrc`: 
  - `$ echo ". $HOME/.asdf/asdf.sh" >> ~/.zshrc` ou
  - `$ echo ". $HOME/.asdf/asdf.sh" >> ~/.bashrc`

### Instalar erlang e elixir
4. Adicionar o plugin do Erlang `$ asdf plugin add erlang`
5. Adicionar o plugin do Elixir `$  asdf plugin add elixir`
6. Instalar o Erlang 23 `$ asdf install erlang 23.3.4.16`
7. Ativar o Erlang `$ asdf global erlang 23.3.4.16`
8. Instalar o Elixir `$ asdf install elixir 1.11.2-otp-23`
9. Ativar o Elixir `$ asdf global elixir 1.11.2-otp-23`

## Instalar o neovim

1. Instalar no OS, para isso usamos os comandos:
 - Windows: `winget install Neovim.Neovim`
 - Mac: `brew install neovim`
 - Ubuntu: `sudo apt-get install neovim`
2. Ir em https://vim-bootstrap.com/ e marcamos as opções:
   1. Elixir
   2. Erlang
   3. JavaScript
   4. HTML
   5. Lua
   6. TypeScript
   7. (Opcional) Vue e Svelte caso queira usar no front
   8. Tema Dracula
   9. Neovim
   10. Gero o arquivo de conf `generate.vim`
3. Moveu o arquivo de conf para a pasta de conf do neovim (varia conforme o Sistema Operacional), no caso:
   1. No Ubuntu: Renomeamos `generate.vim` para `init.vim` e colocamos em `~/.config/nvim`
4. Iniciamos a IDE com `nvim`.

> Caso depois de iniciar o nvim pós-config e não acontecer nada é necessário rodar o comando `:PlugInstall`

## Configurando o LSP
