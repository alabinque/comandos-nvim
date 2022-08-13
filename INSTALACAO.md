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
<details>
  <summary>Caso esteja no Ubuntu (e derivados)</summary>
  
 > Existe um problema de compatibilidade entre a versão do OpenSSL que vem no Ubuntu e a necessaria para compilar o Erlang. Para resolver isso é necessário compilar o OpenSSL e seguir o passo-a-passo abaixo.
```  
$ cd /usr/local/src/
$ sudo wget https://www.openssl.org/source/openssl-1.1.1m.tar.gz

$ sudo tar -xf openssl-1.1.1m.tar.gz
$ cd openssl-1.1.1m
$ sudo ./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl shared zlib
$ sudo make
$ sudo make test
$ sudo make install

# install erlang now
$ export KERL_CONFIGURE_OPTIONS="-with-ssl=/usr/local/ssl"
$ asdf install erlang 23.3.4.16
```
Solução encontrada [nessa issue](https://github.com/asdf-vm/asdf-erlang/issues/247#issuecomment-1114991944).
</details>

7. Instalar o Erlang 23 `$ asdf install erlang 23.3.4.16`
8. Ativar o Erlang `$ asdf global erlang 23.3.4.16`
9. Instalar o Elixir `$ asdf install elixir 1.11.2-otp-23`
10. Ativar o Elixir `$ asdf global elixir 1.11.2-otp-23`

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
   8. Tema Dracul
   9. Neovim
   10. Gero o arquivo de conf `generate.vim`
3. Moveu o arquivo de conf para a pasta de conf do neovim (varia conforme o Sistema Operacional), no caso:
   1. No Ubuntu: Renomeamos `generate.vim` para `init.vim` e colocamos em `~/.config/nvim`
4. Iniciamos a IDE com `nvim`.

> Caso depois de iniciar o nvim pós-config e não acontecer nada é necessário rodar o comando `:PlugInstall`

## Instalando e configurando o LSP
> Antes instale o node caso não tenha `curl -sL install-node.vercel.app/lts | bash`
1. Instalar o `coc.nvim` adicionando a seguinte linha em seu `vim.init`: 
  - `Plug 'neoclide/coc.nvim', {'branch': 'release'}`
2. Rodar o comando `:PlugInstall`
3. Rodar o comando `:CocInstall coc-elixir`
<details>
  <summary>Caso o LSP tenha erro ao iniciar</summary>
  
 > Isso pode acontecer por uma incompatibilidade entre a versão do Erlang que o LSP foi compilado e a versão instalada no seu computador para resolver isso siga o passo-a-passo.

1. Clone e faça a build do projeto.
```
$ git clone https://github.com/elixir-lsp/elixir-ls.git ~/.elixir-ls
$ cd ~/.elixir-ls
$ mix deps.get && mix compile && mix elixir_ls.release -o release
```
2. Abra o `nvim` e entre o comando `:CocConfig` para abrir o arquivo de configuração do coc, então adicione a linha abaixo, salve e feche.
```json
{
  "elixir.pathToElixirLS": "~/.elixir-ls/release/language_server.sh"
}
```
3. Feche e abra novamente o `nvim`, o LSP deve estar funcionando.
</details>

