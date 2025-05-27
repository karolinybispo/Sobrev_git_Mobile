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
- [Commits and version management](#commits-and-version-management)
- [Workflow advanced](#workflow-advanced)
- [Conflict resolution](#conflict-resolution)
- [Case Studies and Best Practices](#case-studies-and-best-practices
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
### Para conseguir enviar a producao do repositorio local , que esta no Vscode, para o GitHub:
- Tenha o [git instalado](#initial-setting) e ja tenha o repositorio criado no github

- Agora, antes de comecar a desenvolver, clone o repositorio remoto no vscode: git clone url-do-repo-remoto

- Ao criar sub-pasta, arquivos ou fazer outra coisa no repositorio local, adicione essas mudancas para o repositorio remoto ficar atualizado: git add .

- Commita as mudancas: git commit -m "mensagem"

- Atualize o repositorio local: git pull

- Empurre para o repositorio remoto: git push

 ### Para enviar o repositorio local que esta no Eclipse para o GitHub:
-  **Configuração Inicial**:
   - Vá para `Window` > `Show View` > `Other...`.
   - Selecione `Git Repositories` e clique em `OK`.
   - Clique com o botão direito no Git Repositories View e selecione `Paste Repository Path or URI`.
   - Cole o URL do repositório Git e clique em `Finish`.
   - Configure seu nome de usuário e email em `Window` > `Preferences` > `Team` > `Git` > `Configuration`.

 **Execução de Operações Git Dentro do Eclipse**
- **Clonagem de Repositório**:
  - Clique em `Clone a Git Repository` no Git Repositories View.
  - Insira o URL do repositório e siga as instruções.

- **Commit de Alterações**:
  - Clique com o botão direito no projeto no Package Explorer.
  - Vá para `Team` > `Commit`.
  - Selecione os arquivos a serem commitados, insira uma mensagem de commit e clique em `Commit`.

- **Push e Pull**:
  - Clique com o botão direito no projeto no Package Explorer.
  - Vá para `Team` > `Remote` > `Pull...` ou `Push...`.
  - Escolha a branch desejada e siga as instruções.



### Para enviar o repositorio local que esta no Android Studio para o GitHub:

1.  **Configuração Inicial**
-  **Inicialização de um Repositório Git**:
   - Abra seu projeto no Android Studio.
   - Vá para `VCS` > `Import into Version Control` > `Create Git Repository`.
   - Selecione a pasta raiz do seu projeto e clique em `OK`.

-  **Configuração do VCS**:
   - Vá para `File` > `Settings` > `Version Control`.
   - Selecione `Git` na lista e configure suas preferências, como email e nome de usuário.

### Execução de Operações Git no Android Studio
- **Commit de Alterações**:
  - Vá para `VCS` > `Commit`.
  - Selecione os arquivos a serem commitados, insira uma mensagem de commit e clique em `Commit`.

- **Push e Pull**:
  - Vá para `VCS` > `Git` > `Push` ou `Pull`.
  - Escolha a branch desejada e siga as instruções.

- **Criação de Branches**:
  - Vá para `VCS` > `Git` > `Branches` > `New Branch`.
  - Insira o nome da nova branch e clique em `OK`.

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

## Commits and version management
1. **Estratégias para commits limpos e eficazes.**
- evite commits desnecessarios;
- divida as alteracoes em unidades logicas e pequenas;
- cada commit deve representar uma unica funcionalidade, correcao ou melhoria;
- escreva a mensagem no commit com um verbo no imperativo (ex: Adicionar, corrigir);
- seja claro, descreva o que foi alterado e por quê;
- Evite commitar arquivos temporários, de configuração ou gerados automaticamente.

## Workflow advanced

**Fluxo de Trabalho Avançado**

#### Backlog
- Lista de tarefas pendentes ou desejadas para um projeto.
- Geralmente organizada por prioridade e necessidade de implementação.

#### Changelog
- Registro de todas as mudanças feitas em um projeto, geralmente listando alterações por versão.
- Ajuda a acompanhar o progresso do desenvolvimento e comunicar as alterações aos usuários.

#### Versionamento em 3 Níveis (X.Y.Z)
- **X**: Versão Principal
  - Incrementada para grandes mudanças ou marcos significativos do projeto.
- **Y**: Versão Secundária
  - Incrementada para adições de funcionalidades ou melhorias significativas.
- **Z**: Versão de Correção
  - Incrementada para correções de bugs ou pequenas melhorias.

Este sistema de versionamento permite uma comunicação clara das mudanças feitas em um projeto e ajuda os usuários a entenderem o impacto das atualizações.

## Conflict resolution




1. **Comunicação Efetiva**:
   - Discuta o conflito abertamente e de forma construtiva.
   - Ouça atentamente todas as partes envolvidas para entender suas perspectivas.

2. **Negociação**:
   - Busque um compromisso que atenda às necessidades de todas as partes.
   - Identifique interesses comuns e explore soluções criativas.

3. **Revisão de Código**:
   - Utilize Pull Requests no GitHub para revisar e discutir mudanças antes de mesclar.
   - A revisão de código antecipada pode prevenir conflitos e melhorar a qualidade do código.

#### Ferramentas

1. **Git Merge Tool**:
   - O Git oferece ferramentas de mesclagem integradas para ajudar na resolução de conflitos de mesclagem.
   - Exemplos incluem `git mergetool`, que pode ser configurado para usar ferramentas visuais como `meld`, `kdiff3` ou `Beyond Compare`.

2. **GitHub Interface**:
   - Use a interface do GitHub para identificar e resolver conflitos em Pull Requests.
   - GitHub fornece uma interface visual para resolver conflitos diretamente no navegador.

3. **IDEs com Suporte a Git**:
   - Muitos IDEs, como Visual Studio Code, IntelliJ IDEA e Eclipse, oferecem recursos integrados para resolver conflitos de mesclagem.
   - Essas ferramentas geralmente fornecem interfaces gráficas que facilitam a visualização e a resolução de conflitos.

4. **Ferramentas de Linha de Comando**:
   - Utilize comandos Git como `git status`, `git diff` e `git mergetool` para identificar e resolver conflitos.
   - Ferramentas como `tig` podem ajudar a visualizar o histórico de commits e entender onde ocorrem os conflitos.


## Case Studies and Best Practices

1 - **Exemplos reais de utilização do Git em projetos de software:**
    
**React (Facebook)**:
   - O projeto React usa Git para colaboração entre desenvolvedores distribuídos globalmente.
   - Utiliza Pull Requests para revisões de código e integração contínua para testes automatizados.

2 - **Dicas para manter a integridade do repositório.**


**Mensagens de Commit Claras e Descritivas**:
   - Escreva mensagens de commit que expliquem claramente o que foi alterado e por quê.
   - Utilize um estilo consistente, como começar com um verbo no imperativo.

**Uso de Branches**:
   - Utilize branches para desenvolver novas funcionalidades, corrigir bugs e experimentar.
   - Mantenha a branch principal (`main` ou `master`) sempre estável e pronta para produção.

**Revisões de Código (Pull Requests)**:
   - Use Pull Requests para revisar o código antes de mesclar nas branches principais.
   - Encoraje feedback construtivo e múltiplos revisores para melhorar a qualidade do código.

**Integração Contínua**:
   - Configure integração contínua (CI) para testar automaticamente as alterações.
   - Certifique-se de que todos os testes passem antes de mesclar mudanças.

**Backup e Recuperação**:
   - Regularmente faça backup do repositório, especialmente para projetos críticos.
   - Utilize tags e releases para marcar versões estáveis e facilitar a recuperação de estados anteriores.

**Documentação e Contribuição**:
   - Mantenha uma documentação clara sobre como configurar e contribuir para o projeto.
   - Forneça diretrizes para contribuidores para garantir um fluxo de trabalho consistente.


## Branch to feature
É a branch destinada para testes, desenvolvimento de nova funcionalidade. Isso nao interfere em nada o codigo principal, pois ê tudo feito em uma branch secundaria. 

Apos a sua utilizacao e merge ela pode ser excluida.
1. para a exclusao, primeiro veja se o merge foi realmente realizado: git log (ele mostra historico de commit e confirma se o merge foi corretamente feito).
2. exclusao local: git branch -d nome-branch-feature (ela so vai ser excluida se tiver sido feito o merge. Com o d maiusculo, com merge ou nao, sera excluido)
3. excluindo do repo remoto: git push origin --delete nome-branch-feature
   
