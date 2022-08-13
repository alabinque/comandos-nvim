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
   8. Tema Dracula
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

Solução encontrada no [README](https://github.com/elixir-lsp/coc-elixir#server-fails-to-start) do projeto.
</details>

4. Adicionar o trecho abaixo em seu `init.vim` para que os atalhos funcionem.
```vim
" Some servers have issues with backup files, see #649.
set nobackup
set nowritebackup

" Having longer updatetime (default is 4000 ms = 4 s) leads to noticeable
" delays and poor user experience.
set updatetime=300

" Always show the signcolumn, otherwise it would shift the text each time
" diagnostics appear/become resolved.
set signcolumn=yes

" Use tab for trigger completion with characters ahead and navigate.
" NOTE: Use command ':verbose imap <tab>' to make sure tab is not mapped by
" other plugin before putting this into your config.
inoremap <silent><expr> <TAB>
      \ coc#pum#visible() ? coc#pum#next(1):
      \ CheckBackspace() ? "\<Tab>" :
      \ coc#refresh()
inoremap <expr><S-TAB> coc#pum#visible() ? coc#pum#prev(1) : "\<C-h>"

" Make <CR> to accept selected completion item or notify coc.nvim to format
" <C-g>u breaks current undo, please make your own choice.
inoremap <silent><expr> <CR> coc#pum#visible() ? coc#pum#confirm()
                              \: "\<C-g>u\<CR>\<c-r>=coc#on_enter()\<CR>"

function! CheckBackspace() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~# '\s'
endfunction

" Use <c-space> to trigger completion.
if has('nvim')
  inoremap <silent><expr> <c-space> coc#refresh()
else
  inoremap <silent><expr> <c-@> coc#refresh()
endif

" Use `[g` and `]g` to navigate diagnostics
" Use `:CocDiagnostics` to get all diagnostics of current buffer in location list.
nmap <silent> [g <Plug>(coc-diagnostic-prev)
nmap <silent> ]g <Plug>(coc-diagnostic-next)

" GoTo code navigation.
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

" Use K to show documentation in preview window.
nnoremap <silent> K :call ShowDocumentation()<CR>

function! ShowDocumentation()
  if CocAction('hasProvider', 'hover')
    call CocActionAsync('doHover')
  else
    call feedkeys('K', 'in')
  endif
endfunction

" Highlight the symbol and its references when holding the cursor.
autocmd CursorHold * silent call CocActionAsync('highlight')

" Symbol renaming.
nmap <leader>rn <Plug>(coc-rename)

" Formatting selected code.
xmap <leader>f  <Plug>(coc-format-selected)
nmap <leader>f  <Plug>(coc-format-selected)

augroup mygroup
  autocmd!
  " Setup formatexpr specified filetype(s).
  autocmd FileType typescript,json setl formatexpr=CocAction('formatSelected')
  " Update signature help on jump placeholder.
  autocmd User CocJumpPlaceholder call CocActionAsync('showSignatureHelp')
augroup end

" Applying codeAction to the selected region.
" Example: `<leader>aap` for current paragraph
xmap <leader>a  <Plug>(coc-codeaction-selected)
nmap <leader>a  <Plug>(coc-codeaction-selected)

" Remap keys for applying codeAction to the current buffer.
nmap <leader>ac  <Plug>(coc-codeaction)
" Apply AutoFix to problem on the current line.
nmap <leader>qf  <Plug>(coc-fix-current)

" Run the Code Lens action on the current line.
nmap <leader>cl  <Plug>(coc-codelens-action)

" Map function and class text objects
" NOTE: Requires 'textDocument.documentSymbol' support from the language server.
xmap if <Plug>(coc-funcobj-i)
omap if <Plug>(coc-funcobj-i)
xmap af <Plug>(coc-funcobj-a)
omap af <Plug>(coc-funcobj-a)
xmap ic <Plug>(coc-classobj-i)
omap ic <Plug>(coc-classobj-i)
xmap ac <Plug>(coc-classobj-a)
omap ac <Plug>(coc-classobj-a)

" Remap <C-f> and <C-b> for scroll float windows/popups.
if has('nvim-0.4.0') || has('patch-8.2.0750')
  nnoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? coc#float#scroll(1) : "\<C-f>"
  nnoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? coc#float#scroll(0) : "\<C-b>"
  inoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? "\<c-r>=coc#float#scroll(1)\<cr>" : "\<Right>"
  inoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? "\<c-r>=coc#float#scroll(0)\<cr>" : "\<Left>"
  vnoremap <silent><nowait><expr> <C-f> coc#float#has_scroll() ? coc#float#scroll(1) : "\<C-f>"
  vnoremap <silent><nowait><expr> <C-b> coc#float#has_scroll() ? coc#float#scroll(0) : "\<C-b>"
endif

" Use CTRL-S for selections ranges.
" Requires 'textDocument/selectionRange' support of language server.
nmap <silent> <C-s> <Plug>(coc-range-select)
xmap <silent> <C-s> <Plug>(coc-range-select)

" Add `:Format` command to format current buffer.
command! -nargs=0 Format :call CocActionAsync('format')

" Add `:Fold` command to fold current buffer.
command! -nargs=? Fold :call     CocAction('fold', <f-args>)

" Add `:OR` command for organize imports of the current buffer.
command! -nargs=0 OR   :call     CocActionAsync('runCommand', 'editor.action.organizeImport')

" Add (Neo)Vim's native statusline support.
" NOTE: Please see `:h coc-status` for integrations with external plugins that
" provide custom statusline: lightline.vim, vim-airline.
set statusline^=%{coc#status()}%{get(b:,'coc_current_function','')}

" Mappings for CoCList
" Show all diagnostics.
nnoremap <silent><nowait> <space>a  :<C-u>CocList diagnostics<cr>
" Manage extensions.
nnoremap <silent><nowait> <space>e  :<C-u>CocList extensions<cr>
" Show commands.
nnoremap <silent><nowait> <space>c  :<C-u>CocList commands<cr>
" Find symbol of current document.
nnoremap <silent><nowait> <space>o  :<C-u>CocList outline<cr>
" Search workspace symbols.
nnoremap <silent><nowait> <space>s  :<C-u>CocList -I symbols<cr>
" Do default action for next item.
nnoremap <silent><nowait> <space>j  :<C-u>CocNext<CR>
" Do default action for previous item.
nnoremap <silent><nowait> <space>k  :<C-u>CocPrev<CR>
" Resume latest coc list.
nnoremap <silent><nowait> <space>p  :<C-u>CocListResume<CR>
```

