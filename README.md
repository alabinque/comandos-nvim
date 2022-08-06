# comandos-nvim

# Instalação

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

# Iniciar / Criar Arquivo

Para iniciar a edção de um arquivo ou criar um arquivo novo usamos

`nvim <caminho/nome_do_arquivo>`

Ex: Para criar um arquivo Elixir chamado `despachante.elx` o comando é `nvim despachante.elx` que vai criar na pasta em que o terminal está.

# Modo de Comando

Usam `ESC` para entrar no modo de comando que é onde vocês inserem os comandos do VIM

### Comandos Principais

| Comando | O que faz |
|---------|-----------|
|`:q`     | Sair      |
|`:w`     | Salvar    |
| `:wq`   | Salvar e sair|
| `:q!`   | Sair sem salvar (forçado) |
| `:e <caminho> | Abre o arquivo no vim |
| `:term` ou `:terminal` | Abre o terminal no Vim | 

### Comandos de Pesquisa e Substituição
| Comando | O que faz |
|---------|-----------|
|`/<palavra>`     | Pesquisa <palavra no arquivo> |
|`n`     | Próxima ocorrência de palavra |

# Modo de Edição

Usa `i` para entrar no modo de edição onde vamos inserir o código.

| Comando | O que faz |
|---------|-----------|
|`o`     | Entra no modo de inserção na linha de baixo. |

# Comandos de Interface

| Comando | O que faz |
|---------|-----------|
|`F3`     | Abre/Fecha arquivos do projeto      |
|`F2`     | Busca arquivos na barra de arquivos |

