# commit-pattern

Esse documento tem como objetivo apresentar uma solução para a padronização de mensagens de commit o durante o desenvolvimento e versionamento de software.

Para isso, usaremos como referência o [Conventional Commits v.1.0.0](https://www.conventionalcommits.org/en/v1.0.0/)

## Por que padronizar mensagens de commit?

Por padrão, é possível escrever qualquer tipo de mensagem de commit ao versionar o código. O problema de utilizar palavras extremamente sucintas ou apenas adicionar uma mensagem para garantir que o código esteja versionado, é que revisitar os commits torna-se muito trabalhoso, uma vez que as mensagens não necessáriamente estão muito claras.

![problem](/assets/git/commit-pattern/problem.png)

Na imagem acima, temos mensagens causas por um `merge` que não dizem exatamente quais features foram adicionadas a branch. Temos também, commits que não exemplificam o que foi alterado, como por exemplo `commit message bugfix`, gerando perguntas como:
> Qual bug foi corrigido?

Para que exista maior clareza de leitura, identificação e até mesmo documentação, é necessário que existam padrões na hora de escrita da mensagem do commit.

## Como funciona o padrão proposto pelo Conventional Commits v1.0.0?

> Referência: [Conventional Commits v.1.0.0 specification](https://www.conventionalcommits.org/en/v1.0.0/#specification)

O commit deve ser estruturado da seguinte maneira:

> < type >[optional scope]: < description >
>
>[optional body]
>
>[optional footer(s)]

O commit deve conter os seguintes elementos estruturais, para deixar claro aos consumidores:

1. fix: Um commit com o tipo `fix` refere-se a correção de um `bug` no código (seria equivalente ao `PATCH` no `Semantic Versioning`);
2. feat: Um commit com o tipo `feat` refere-se a adição de uma nova feature no código (equivalente ao `MINOR` no `Semantic Versioning`);
3. BREAKING CHANGE: um commit com o footer `BREAKING CHANGE:`, ou com `!` logo após o `tipo ou escopo`, representa  uma breaking change no código (equivalenta ao `MAJOR` no `Semantic Versioning`);
4. Outros tipos recomendados podem ser (baseados no [Angular Convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)):
    - build:
    - chore:
    - docs:
    - style:
    - refactor:
    - perf:
    - test:
    ...
5. Footers que não `BREAKING CHANGE: <description>` podem exitir, seguindo a convenção equivalente ao [git trailer format](https://git-scm.com/docs/git-interpret-trailers)  

Tipos adicionais não são obrigatórios pelas especificações do `Conventional Commits`, e não tem efeitos no `Semantic Versioning` (a menos que inclua `BREAKING CHANGE`)

Um escopo pode ser provido por um `commit type`, e caso necessário informações adicionais, deve ser adicionado após o tipo entre parênteses, como no exemplo:

> feat(parser): add ability to parse arrays

## Exemplos

Exemplo do histórico de commits
![example1](/assets/git/commit-pattern/example1.png)

Exemplo da descrição com BREAKING CHANGE
![example2](/assets/git/commit-pattern/example2.png)

Exemplo com descrição e footer

![example3](/assets/git/commit-pattern/example3.png)

## Vantagens de se utilizar Conventional Commits

- Gerar automaticamente `CHANGELOGs`
- Determinar automaticamente o aumento de versão semântica (baseados nos tipos de commits adicionados)
- Comunicar a natureza das mudanças aos membros do time, publico ou stakeholders
- Adiciona processos de build e publicação
- Facilita para que pessoas contribuam com o projeto, possibilitando uma visualização mais estruturada do histórico de commits

##EXTRA: Gitmoji

Uma adicão ao `Conventional Commits` para trazer a opção de descrição **visual** é a utilização em conjunto com [Gitmoji](https://gitmoji.dev)

Dessa forma, a leitura do histórico fica um pouco menos cansativa e mais descritiva pelo atributo visual.

![example4](/assets/git/commit-pattern/example4.png)