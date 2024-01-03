# project-strategy

Esse documento tem como objetivo apresentar uma solucão para a estratégia o versionamento durante o desenvolvimento de software.

Utilizaremos `git` como sistema de controle de versão.

## Histórico de commits

Para utilizar git, existem diversos comandos para poder se versionar. Cada comando altera a `árvore de commits` de uma forma diferente. Para esse exemplo, iremos focar e exemplificar como ficaria a `árvore de commits` nos comandos:

- [merge](#git-merge);
- squash;
- rebase;

### git merge

Seguindo o exemplo:

![merge-tree](/assets/merge/merge-tree.png "merge-tree")

Existiram alterações na branch `main` que crairam um conflito com a branch `change-readme`.

![merge-conflict](/assets/merge/merge-conflict.png "merge-conflict")

Para poder continuar com o `Pull request`, será necessário resolver o conflito na branch `change-readme` para então fazer o merge com a main.

Uma das formas de resolver esse problema, é atualizar a branch `main` e executar o comando merge na branch `change-readme`
> git merge main

Ao finalizar esse processo, a `Árvore de commits` ficará da seguinte forma:

![merge-update](/assets/merge/merge-update.png "merge-update")

e por fim, ao executar o merge do `pull request`, teremos:

![merge-pr](/assets/merge/merge-pr.png "merge-pr")

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
![merge-chaos](/assets/merge/merge-chaos.png "merge-chaos")

> Após executar o merge de todas as branchs abertas

![merge-chaos2](/assets/merge/merge-chaos2.png)

Em um primeiro instante, podemos ver a inconstência da `Arvore de commits`, uma vez que na primeira imagem, a primeira linha (azul) refere-se a branch `v1`, mas após atualizar todas as branchs, a primeira linha (azul) é a branch `main`

### git squash