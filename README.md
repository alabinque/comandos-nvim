# comandos-nvim

# Instalação

1. Instalar no OS, para isso usamos os comandos:
 1. Windows: `winget install Neovim.Neovim`
 2. Mac: `brew install neovim`
 3. Ubuntu: `sudo apt-get install neovim`
2. Ir em https://vim-bootstrap.com/ e marcamos as opções:
 1. Elixir
 2. Erlang
 3. JavaScript
 4. HTML
 5. Lua
 6. TypeScript
 7.(Opcional) Vue e Svelte caso queira usar no front
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

| Comando | O que faz |
|---------|-----------|
|`:q`     | Sair      |
|`:w`     | Salvar    |
| `:wq`   | Salvar e sair|
| `:q!`   | Sair sem salvar (forçado) |

# Modo de Edição

Usa `i` para entrar no modo de edição onde vamos inserir o código.

