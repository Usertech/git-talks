title: GIT talk 02
author:
  name: Lukáš Rychtecký
  twitter: lukasrychtecky
controls: true
style: style.css

--

# GIT - náš denní chléb
## Talk 02
## Lukáš Rychtecký
## [https://twitter.com/LukasRychtecky](https://twitter.com/LukasRychtecky)

--

### Obsah

* Résumé
* Distribuovaný vs. Centralizovaný
* GIT uvnitř
* Větve a workflow
* Klonování a můj repozitář
* Rebase a merge
* Diff a tig
* Checkout a reset
* Reflog, stash a blame
* Konfig a aliasy
* Reference

--

### Résumé

* `add` - připraví soubory ke commitu
* `commit` - vytvoří novou revizi
* `pull` and `push` - synchronizuje repozitář
* `status` - zobrazí stav, změny apod.
* `diff` - zobrazí konkrétní změny v souborech
* `log` - procházení historie

--

### Distribuovaný vs. Centralizovaný

#### Centralizovaný

* jeden hlavní repozitář (master-slave)
* hlavní repozitář vytváří bottle-neck
* nemožnost práce offline, pomalá odezva (závislé na rychlosti připojení)
* příklady: CVS, SVN

--

### Distribuovaný vs. Centralizovaný

#### Centralizovaný

![Centralizovaný](img/cvcs.png)

--

### Distribuovaný vs. Centralizovaný

#### Distribuovaný

* sít propojených repozitářů (peer-to-peer)
* žádný repozitář není opravdu "hlavní"
* práce offline, lokálně dostupná historie, rychlost
* příklady: GIT, Mercurial

--

### Distribuovaný vs. Centralizovaný

#### Distribuovaný

![Distribuovaný](img/dvcs.png)


--

### GIT uvnitř

Historie v GITu je uložena jako acyklický orientovaný graf

![DAG](http://cdn.meme.am/instances/500x/55967408.jpg)

--

### GIT uvnitř

* celý projekt je uložen ve snímcích (snapshots)
* listy grafu jsou revize (snímky) a hrany ukazují na předchozí revizi (nejstarší vlevo)

![GIT graf](http://think-like-a-git.net/assets/images2/reachability-example.png)

--

### GIT uvnitř

Příklad `git log --oneline --graph`

![GIT log](img/git-graph.png)

--

### Větve a workflow

* větve umožňují paralelní vývoj
* snadné a rychlé přepínání mezi větvemi
* vytvoření větve `git branch <název-větve>`
* přepnutí do větve `git checkout <název-větve>`
* lze zkrátit `git checkout -b <název-větve>`
* best practice - vytvářet větev na každou funkcionalitu

![Git branch](https://www.atlassian.com/wac/landing/git/tutorial/git-branches/pageSections/0/contentColumnTwo/0/imageBinary/git-tutorial_branching-merging.png)

--

### Větve a workflow

![Git branch](https://i.imgflip.com/zb4dt.jpg)

--

### Klonování a můj repozitář

#### Začátek práce na projektu

* klonování - origin (z něj se stahují změny) `git clone git@bitbucket.org:usertech/kup-najisto.git`
* přidání public repozitáře (do něj se pushují změny) `git remote add public git@bitbucket.org:lukas_rychtecky/kup-najisto.git`
* zobrazní připojených repozitářů `git remote -v`

--

### Rebase a merge

#### Rebase

* aktualizuje větev aplikováním jednotlivých revizí
* `git rebase master`

![GIT rebase](http://rypress.com/tutorials/git/media/5-1.png)

--

### Rebase a merge

#### Rebase

* příklad: chci poslední commit sloučit s předchozím
* `git rebase -i HEAD~2` - spustí interaktivní rebase od současné verze (HEAD) o 2 revize zpět

![GIT rebase -i](img/git-rebase-i.png)

--

### Rebase a merge

#### Rebase vs. commit

* sloučení změn s předchozí revizí lze udělat i při commitu
* `git commit --ammend`
* připravené změny sloučí s předchozí revizí

--

### Rebase a merge

#### Interaktivní rebase umožňuje

* změnu pořadí revizí (commitů)
* změnu commit zpráv
* odstranění a sloučení commitů

--

### Rebase a merge

#### Rebase - řešení problémů

* během `rebase` se můžou objevit konflikty
* vyřeším konflikty `git add <soubory>` a `git rebase --continue`
* v případě problémů zastavím `rebase` - `git rebase --abort`

--

### Reference

* [Git Workflow](http://nvie.com/posts/a-successful-git-branching-model/)
* `man git` or `git help`
* https://git-scm.com/ - official website
* [Pro GIT](https://git-scm.com/book/en/v2) - ask me for czech version in PDF
* Git guide - https://backlogtool.com/git-guide/en/
* Git game (advanced) - [http://pcottle.github.io/learnGitBranching/](http://pcottle.github.io/learnGitBranching/)
* This presentation [https://github.com/LukasRychtecky/git-talks/](https://github.com/LukasRychtecky/git-talks/)

--

### Thanks for your attention

![Linus Torvalds](http://cdn.meme.am/instances/22164438.jpg)
