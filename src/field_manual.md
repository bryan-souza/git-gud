# Manual de Campo

Aqui estarei colocando um resumo dos comandos básicos para a execução do *workflow* git

## Adicionar um repositório GIT à sua máquina

Comandos usados para começar a trabalhar com git.

### Clone

Usado para clonar (basicamente baixar) um repositório remoto para sua máquina.

```shell
git clone [url] [destino]
```

#### Exemplos

```shell
# GitHub
git clone https://github.com/bryan-souza/git-gud.git
git clone git@github.com:bryan-souza/git-gud.git

# GitLab
git clone https://gitlab.com/user/repo.git
git clone git@gitlab.com:user/repo.git
```

### Init

Usado para inicializar um novo repositório git localmente.

```shell
git init [nome_do_repositorio]
```

#### Exemplos

```shell
# Inicializar um repositório chamado 'openbooks'
git init openbooks

# Inicializar um repositório chamado 'dotfiles' e alterando o nome da
# branch principal para 'main'
git init dotfiles -b main
```

---

## Lidando com *branches*

Comandos para listar, criar, excluir, renomear e trocar de *branch*.

### Mostrar *branch* atual

```shell
git branch --show-current
```

### Listar *branches*

```shell
# Listar branches locais
git branch --list

# Listar branches remotas
git branch --remotes

# Mostrar todas as branches (locais + remotas)
git branch --all
```

### Criar uma *branch*

```shell
git branch [branch_base] [branch_nova]
```

> Nota: se você omitir o parâmetro `[branch_base]`, a nova *branch* será criada com base na *branch* atual

#### Exemplos

```shell
# Criar uma branch chamada 'v2.0' a partir da branch atual
git branch v2.0

# Criar uma branch chamada 'nova_feature' a partir da branch 'master'
git branch master nova_feature
```

### Renomear uma *branch*

```shell
git branch --move [nome_antigo] [nome_novo]
```

### Remover uma *branch*

```shell
# Renomear a branch para corrigir um erro de digitação
git branch --delete [nome_da_branch]
```

> Nota: a *branch* deve ter sido mesclada (*merged*) completamente à *upstream* ou estar igual (no mesmo *commit*) que a mesma. Caso contrário é preciso usar a flag `--force` para forçar a remoção.

### Trocar de *branch*

```shell
git switch [branch]
git checkout [branch]
```

> Nota: Sim, tem dois comandos para fazer a mesma coisa. A diferença é que `checkout` realiza outras ações além de simplesmente trocar de *branch*, enquanto `switch` apenas faz a troca.

### Mesclar *branches*

Aplicar as mudanças de outra *branch* na *branch* atual, fundindo as duas em um *commit*

> Nota: `merge` é o comando mais complexo que tem no git na minha opinião, e por consequência é o que mais dá erro. Pretendo dedicar uma seção inteira para explicar como funciona e como resolver conflitos, mas como a função de um 'manual de campo' é mostrar o comando, aqui está.

```shell
git merge [branch]
```

### Reset

Reverte as alterações da branch atual para o estado de HEAD ou para um commit específico.

> Aviso: esse comando pode ser DESTRUTIVO!

```shell
git reset [commit]
```

#### Exemplos

```shell
# Reseta o indice da branch para o estado de HEAD, mantendo suas
# alterações e sinalizando quais arquivos foram revertidos
git reset
git reset --mixed

# Reseta o índice da branch para o estado de HEAD, deixando seus
# arquivos marcados como 'unstaged'
git reset --soft

# Reseta o índice e os arquivos da branch para o estado de HEAD,
# descartando qualquer mudança realizada
git reset --hard

# Reseta a branch e o índice como há 5 commits atrás
git reset HEAD~5
```

---

## Lidando com modificações

Comandos para visualizar, adicionar e remover modificações feitas ao índice da *working tree* atual.

### Status

Mostra o estado atual da *working tree* (quais arquivos foram adicionados e ainda não foram adicionados ao repositório; quais arquivos foram modificados; e quais arquivos foram excluídos do repositório)

```shell
git status
```

### Add

Prepara os arquivos para serem adicionados à *working tree*.

```shell
git add [nome_do_arquivo]
```

#### Exemplos

```shell
# Adicionar todas as mudanças à working tree
git add .

# Adicionar um arquivo chamado 'index.html'
git add index.html

# Adicionar uma pasta chamada 'docs' e todos os arquivos dentro dela
git add docs
```

### Rm

Remove um arquivo ou diretório da *working tree*.

```shell
git rm [arquivo]
```

> Nota: esse comando não apaga os arquivos do seu sistema, ele apenas os remove do índice, fazendo com que sejam marcados como `untracked` após um *commit*.

#### Exemplos

```shell
# Remover o arquivo 'main.rs' do índice
git rm main.rs

# Remover o diretório 'docs', mas preservar seu conteúdo
git rm docs

# Remover o diretório 'build' e todo o seu conteúdo
git rm -r build
```

### Stash

Adiciona arquivos modificados para uma `stash` para uso posterior e reseta a *working tree* para o estado de HEAD.

```shell
git stash # Insere todos os arquivos modificados em uma stash
git stash -- [arquivo] # Insere apenas [arquivo] em uma stash
```

### Stash list

Lista todas as `stashes` criadas.

```shell
git stash list
```

### Stash show

Mostra quais arquivos estão inseridos em uma `stash`

```shell
git stash show [stash]
```

> Nota: `[stash]` é o nome da `stash`; obtido com `stash list`.

### Stash apply

Aplica as mudanças de uma `stash` na *working tree*, sobrescrevendo os arquivos sem retirar os arquivos da mesma ou apagá-la. (É como 'copiar e substituir')

```shell
git stash apply [stash]
```

### Stash pop

Mesma função do `stash apply` com a diferença que, nesse caso, os arquivos são removidos da `stash` e a mesma é apagada.

```shell
git stash pop [stash]
```

### Commit

Adiciona todas as modificações adicionadas com `add` para o índice da *working tree*.

```shell
git commit -m "[mensagem]"
```

> Nota: o comando `commit` precisa de uma mensagem para funcionar, seja usando a flag `-m`, seja usando a flag `--interactive`

#### Exemplos

```shell
# Commit com uma mesagem básica
git commit -m "Adicionado index.html"

# Commit adicionando todas as modificações
git commit -am "Adicionado index.html"

# Commit interativo:
# Abre um editor de texto para adicionar arquivos ao indice
# e editar a mensagem do commit
git commit --interactive
```

### Rebase

Usado para mesclar *commits* em um só (*squash*) ou para fazer modificações em como as *branches* se dispõem.

> Nota: estou colocando junto com os comandos para aplicar mudanças à *working tree* pois esse comando geralmente é usado para *squashing* de *commits*, e não para re-arranjar a *working tree*.

```shell
# Sugestão: sempre que possível, use a flag --interactive;
# vai facilitar e muito a sua vida!
git rebase --interactive [após-esse-commit]
```

> Nota: `rebase` é outro daqueles comandos um pouco complexos que precisam de atenção especial. Por esse motivo, estarei dedicando uma seção para falar sobre como melhorar seus commits com `rebase` e `squash`

---

## Trabalhando com *remotes*

Comandos usados para administrar repositórios remotos (*remotes*) e aplicar mudanças local -> remoto e remoto -> local.

### Remote add

Adiciona uma URL remota ao repositório.

```shell
git remote add [nome] [url]
```

#### Exemplos

```shell
# Adicionar um remote chamado 'origin' com uma url do GitHub
git remote add origin https://github.com/bryan-souza/openbooks.git
```

### Fetch

Baixa atualizações de *branches*, *tags* e *commits* de um ou vários *remotes*

```shell
git fetch
```

### Push

Usado para aplicar as mudanças locais no repositório remoto

```shell
git push
```

> Nota: é preciso configurar um repositório remoto caso tenha inicializado localmente com `git init`. Caso o repositório tenha sido clonado, não é preciso configurar.

### Pull

Aplica as mudanças feitas no repositório remoto ao seu repositório local.

> Aviso: esse comando pode ser DESTRUTIVO!

```shell
git pull
```

> Nota: para evitar a perda de suas modificações locais, sugiro que faça isso:

```shell
git stash
git pull
git stash pop
```

> Nota: a diferença entre `fetch` e `pull` é que `fetch` é considerado uma opção segura para baixar as atualizações do repositório, visto que não é destrutivo e não descarta suas alterações, diferente do `pull`.
