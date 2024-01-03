# git-strategy

Esse documento tem como objetivo apresentar uma solucão para a estratégia o versionamento durante o desenvolvimento de software.

Utilizaremos `git` como sistema de controle de versão e a plataforma `github`para os exemplos. 

## Histórico de commits

Para utilizar git, existem diversos comandos para poder se versionar. Cada comando altera a `árvore de commits` de uma forma diferente. Para esse exemplo, iremos focar e exemplificar como ficaria a `árvore de commits` nos comandos:

- [merge](#git-merge);
- [squash](#git-squash);
- rebase;

### git merge

Seguindo o exemplo:

![merge-tree](/assets/git/merge/merge-tree.png "merge-tree")

Existiram alterações na branch `main` que crairam um conflito com a branch `change-readme`.

![merge-conflict](/assets/git/merge/merge-conflict.png "merge-conflict")

Para poder continuar com o `Pull request`, será necessário resolver o conflito na branch `change-readme` para então fazer o merge com a main.

Uma das formas de resolver esse problema, é atualizar a branch `main` e executar o comando merge na branch `change-readme`
> git merge main

Ao finalizar esse processo, a `Árvore de commits` ficará da seguinte forma:

![merge-update](/assets/git/merge/merge-update.png)

e por fim, ao executar o merge do `Pull request`, teremos:

![merge-pr](/assets/git/merge/merge-pr.png)

**Prós de se utilizar essa estratégia**
- Necessita de apenas uma revisão de código quando tiver conflito.
- Simples de executar.
- Só existirá perda de código se durante a resolução do conflito algo for apagado.

**Contras de se utilizar essa estratégia**
- O comando merge cria novos commits ao ser executado. No exemplo:
    > Merge branch 'main' into change-readme

    Por conta disso, ocorre uma poluição visual na `Árvore de commits`
- A longo prazo, torna-se inviável olhar para commits mais antigos pela complexiadade de observar a origem, o histórico de modificações e em que momento cada branch foi atualizada.
- Para fazer rollback, é necessário existir `tags` muito bem definidas, pois voltar para uma determinada hash de um commit não garante que todas as modificações desejadas estejam no determinado ponto.

- Em um projeto onde muitas pessoas pessoas atualizam, a `Árvore de commits` pode ficar da seguinte forma

> Antes de fazer o merge da primeira branch criada a partir da main
![merge-chaos](/assets/git/merge/merge-chaos.png)

> Após executar o merge de todas as branchs abertas

![merge-chaos2](/assets/git/merge/merge-chaos2.png)

Em um primeiro instante, podemos ver a inconstência da `Arvore de commits`, uma vez que na primeira imagem, a primeira linha (azul) refere-se a branch `v1`, mas após atualizar todas as branchs, a primeira linha (azul) é a branch `main`

### git squash

Seguindo o exemplo anterior, digamos que cria-se uma nova branch, mas ao invés de utilizar `merge` para concluir o `Pull request`, seja utilizado `squash`

Durante o processo de `Pull resquest` teríamos a `Árvore de commits` da seguinte forma:

![squash-tree](/assets/git/squash/squash-tree.png)

A branch `v2` terá conflito ao tentar concluir o `Pull request`. Ainda utilizaremos a estratégia de `merge` para atualizar a branch.

![squash-merge](/assets/git/squash/squash-merge.png)

Ao executar o `Pull request`, ao invés de utilizar `merge`, será feito `squash` da branch na main.

![squash-pull-request](/assets/git/squash/squash-pull-request.png)

E por fim teremos a `Árvore de commits` da seguinte forma: 

![squash-end](/assets/git/squash/squash-end.png)

O processo de fazer `squash` durante o `Pull request` pegará **todos** os commits da branch e adicionará na `main` um novo commit com todas as modificações que estavam no `Pull request`.

**Prós de se utilizar essa estratégia**
- Necessita de apenas uma revisão de código quando tiver conflito. (mesma coisa que `merge`)
- Simples de executar.
- Só existirá perda de código se durante a resolução do conflito algo for apagado.
- Ao fazer rollback, existe a garantia de que a feature inteira será retirada, uma vez que os commits da `main` estão unificados em um bloco só.
- Uma `Árvore de commits` mais limpa se comparada com `merge`

![squash-tree-end](/assets/git/squash/squash-tree-end.png)

**Contras de se utilizar essa estratégia**
- Na branch principal, teremos apenas um commit contendo uma feature como um todo, com muito código ao invés de ter vários commits menores dentro de seus determinados contextos.
- Existe uma alta complexiadade para poder dar rollback ou rever código do histórico de commits, uma vez que os commits na `main` tendem a ficar muito maiores.
