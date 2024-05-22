# Sobrev Git/GitHub Mobile

## Temas
- [Various Branches](#various-branches)
- [Navegate between branches](#navegat-between-branches)
- [Maintenance Location and remote producion](#maintenance-location-and-remote-producion)
- [Vscode, Eclipse and Android Studio](#various-branches)
- [Tag of version](#tag-of-version)
- [Commits intermediaries](#commits-intermediaries)
- [Initial setting](#initial-setting)
- [Repository Git: local and remote](#repository-git-local-and-remote)
- [Branch to feature](#branch-to-feature)
- [Branch to feature](#branch-to-feature)
- [Branch to feature](#branch-to-feature)
- [Branch to feature](#branch-to-feature)
- [Branch to feature](#branch-to-feature)
- [Branch to feature](#branch-to-feature)

## Various Branches
Branches: ramos em um repositorio. 
1. Uma nova branch é criada partir da branch principal (main): git branch nome-da-branch.

2. Enviando os commits para o repositorio remoto: git push origin nome-da-branch (depois de fazer esse upstream, você pode usar: git push)

3. Listando as branches do repositorio local: git branch

git branch -a (lista as branchs existentes no repo remoto)


### uso da branchs em ambiente de  desenvolvimento:
Branch principal: 'main ou master'. Fica o codigo estavel e pronto para producao. 

Branch de Desenvolvimento: 'develop'. Base para novas funcionalidades e melhorias.
Aqui, integração e testes sao feitos antes de se mover para a produção.

Feature Branches: 'feature/nome-da-funcionalidade'. Criada(s) a partir de develop para desenvolver novas funcionalidades.
Fundidas de volta em develop após conclusão e revisão.

### uso da branchs em ambiente de producao:
Branch de Produção: 'main ou master'.
Contém o código que está em produção.
Atualizado a partir de develop quando uma versão está pronta para ser lançada.

Hotfix Branches: 'hotfix/nome-do-hotfix'.
Criadas a partir de 'main' para corrigir problemas críticos em produção.
Fundidas de volta em main e develop após a correção

#### USO PRATICO:
1- Desenvolvimento de Funcionalidades:

- Crie uma feature branch: git checkout -b feature/nova-funcionalidade develop.

- Desenvolva e teste a funcionalidade.

- Mescle a feature branch de volta em develop: git checkout develop seguido de git merge feature/nova-funcionalidade.

2- Preparação para Produção:

- Teste e integre todas as funcionalidades na branch develop.

- Quando estiver pronto para produção, mescle develop em main: git checkout main seguido de git merge develop.

3- Correção de Problemas em Produção:

- Crie uma hotfix branch: git checkout -b hotfix/correção-critica main.

- Aplique e teste a correção.

- Mescle a hotfix branch de volta em main e develop: git checkout main seguido de git merge hotfix/correção-critica, depois git checkout develop e git merge hotfix/correção-critica.





## Navegate between branches
Para navegar/mudar entre as branches: git checkout nome-da-branch-desejada.

- Depois de ter feito o commit em uma branch e desejar que essa atualizacao esteja presente na outra branch, de um merge. Siga os passos:
1. esteja na branch de destino.
2. depois, digite: git merge nome-da-branch (essa branch é a de origem).
- se houver conflitos, resolva-os manualmente, conclua o merge e empurre para o repositorio remoto.


## Maintenance Location and remote producionl
Local de manutencao é uma nova branch que serve para testar, resolver bugs e desenvolver. Dessa forma, a branch de producao fica com o codigo ja testado e estavel que sera levada para uso do usuario.

Producao remota é onde o codigo finalizado é implementado para ser utilizado pelo usuario final.

## Vscode, Eclipse and Android Studio
Para enviar a producao do repositorio local , que esta no Vscode, para o GitHub:
- Tenha o [git instalado](#initial-setting) e (nesse contexto, voce ja esta com o repositorio clonado no vscode, se nao estiver, siga isso)

- Para clonar o repositorio remoto no local: git clone url-do-repo-remoto

- Ao criar sub-pasta, arquivos ou fazer outra coisa no repositorio, adicione essas mudancas para o repositorio remoto ficar atualizado: git add .

- Commita as mudancas: git commit -m "mensagem"
- Atualize o repositorio local: git pull
- Empurre para o repositorio remoto: git push

Para enviar o repositorio local que esta no Eclipse para o GitHub:
- siga o tutorial: https://www.youtube.com/watch?v=CMW8ZY1JpnI

Para enviar o repositorio local que esta no Android Studio para o GitHub:
- siga o tutorial: https://www.youtube.com/watch?v=IY9Dex5L5_I

## Tag of version
A tag de versao especifica/etiqueta um estado especifico do codigo. 
Geralmente defini-se um numero que marca a versao do codigo.

Comandos:
- o estado atual do codigo vai receber uma tag e mensagem: git tag -a v1.0.0 -m "tag da primeira versao"
- lista as tags: git tag
- detalhes de uma tag especifica: git show nome-tag
- deletando tag localmente: git tag -d nome-tag
- enviando tag para repo remoto: git push origin v1.0.0

## Commits intermediaries
Isso sgnifica que os commits intermediarios devem ser mantidos apenas na branch de desenvolvimento e nao na branch de producao/principal (que seria a main).
Esses commits intermediarios sao commits de progresso de um trabalho ainda em andamento, se eles ficarem na branch principal acaba poluindo o ambiente e atrapalhando. 
 
Ao estar na branch de desenvolvimento e dar merge na main, os commits desnecessarios irao junto. A solucao para isso nao acontecer é: 
1. esteja na branch de destino
2. no terminal: git merge --squash nome-branch-desenvolvimento
3. faça o commit com uma mensagem simples e que identifique essa melhoria/resolucao de bug etc.

Isso vai evitar os possiveis -inumeros- commits da branch de origem (ou desenvolvimento).

## Branch to feature
É a branch destinada para testes, desenvolvimento de nova funcionalidade. Isso nao interfere em nada o codigo principal, pois é tudo feito em uma branch secundaria. 

- Apos merge ela pode ser excluida.
1. para a exclusao, primeiro veja se o merge foi realmente realizado: git log (ele mostra historico de commit e confirma se o merge foi corretamente feito).
2. exclusao local: git branch -d nome-branch-feature (ela so vai ser excluida se tiver sido feito o merge. Com o d maiusculo, com merge ou nao, sera excluido)
3. excluindo do repo remoto: git push origin --delete nome-branch-feature

## Initial Setting
Instalando o git

1- BAIXE:

- macOS: Você pode instalar o Git usando o Homebrew. Se não tiver o Homebrew instalado, instale-o primeiro seguindo as instruções no site oficial (https://brew.sh/). Depois, no terminal, digite:
brew install git

2- INSTALE:
- macOS e Linux: Se você usou os comandos acima, o Git será instalado automaticamente.

3- CONFIGURACAO INICIAL DO GIT

- Abra o terminal e configire o nome de usauario: git config --global user.name "Seu Nome"

- Configurando o e-mail: git config --global user.email "seu.email@example.com"

Essas configurações são salvas no arquivo de configuração do Git e serão usadas para todos os repositórios que você criar ou contribuir.

4- VERIFICANDO AS CONFIGURACOES:

- Este comando "git config --global --list" exibirá uma lista com as configurações globais do Git, incluindo seu nome de usuário e email.

## Repository Git: local and remote

1- Crie um repositorio remoto:

- vá ate sua conta no github, crie um repositorio e copie a URL do repositorio.

2- Clonando o repositorio:

- se estiver usando VScode, no terminal digite: git clone URL-do-repositório

Diferenca entre repositorio local e remoto: 
 
 1- Local:
 - armazenado no seu proprio computador;

 - usado para desenvolvimento e controle de versao individual.

 2- Remoto:

 - armazenado em servidores externos(ex: github);

 - facilita colaboracao e beckup.





