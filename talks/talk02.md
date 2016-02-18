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
* Další praktické vychytávky

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

<img src="http://cdn.meme.am/instances/500x/55967408.jpg" width="300">

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

* chtěli jste někdo změni historii? S GITem můžete již dnes!
* aktualizuje větev aplikováním jednotlivých revizí
* `git rebase master`
* `rebase` mění historii, proto je nutné při `push` použít `-f`
* příklad `git push -f public <název-větve>`

--

### Rebase a merge

#### Rebase - Jak funguje?

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
* `git commit --ammend
* `ammend` mění historii při `push` nutné použít `-f`
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

### Rebase a merge

#### Merge

* sloučení dvou větví
* provádí ten, kdo merguje pull request
* `git merge <moje-větev>` - vytvoří lineární se základní větví
* `git merge --no-ff <moje-větev>` - vytvoří "merge commit" (čitelnější historie)

--

### Rebase a merge

#### Merge vs. no-ff

<img src="http://i.stack.imgur.com/FMD5h.png" width="500">

--

### Rebase a merge

#### Merge vs. rebase

* `merge --no-ff` - když merguju větev do hlavní větve (master, dev apod.)
* `rebase` - chci aktualizovat větev vůči hlavní větvi (99 % případů)

--

### Diff a tig

#### Diff

* `git diff` - zobrazí změny na `HEAD`
* pozor zobrazí pouze soubory, o kterých GIT ví a nejsou přípravené ke commitu (`git add`)
* umí zobrazit změny mezi revizemi, např. `git diff d06ab07..1978aa3`
* `git diff --cached` - zobrazí změny na `HEAD` připravené ke commitu

--

### Diff a tig

#### tig

* nástroj pro zobrazení historie v konzoli [https://github.com/jonas/tig](https://github.com/jonas/tig)
* funguje skvěle nejen na serveru, ovládání jako Vim <3

![tig](https://gitfu.files.wordpress.com/2008/05/tig-maindiffsplit.png)

--

### Checkout a reset

#### Checkout

* přepínání mezi větvemi - `git checkout <moje-větev>`
* vytvoří větev a přepne do ní - `git checkout -b <nová-větev>`
* umí přepnout do kterékoliv revize - `git checkout 1978aa3`
* zahození změn - `git checkout -- <název-souboru>`

--

### Checkout a reset

#### Checkout

* v GITu lze používat shellové wildcards - `git checkout -- *.py`
* zahození všech změn - `git checkout -- .`
* zahodí pouze změny, které nejsou připraveny ke commitu

--

### Checkout a reset

#### Reset

* resetuje `HEAD` na konkrétní revizi
* odsun změn připravených ke commitu - `git reset HEAD *.py`
* nezahazuje změny jako `git checkout`
* `git reset HEAD~1` - zahodí poslední commit, ale ponechá změny
* `git reset --hard origin/master` - natvrdo resetuje HEAD vůči `origin/master`

--

### Reflog, stash a blame

#### Reflog

* z GITu nelze "nic smazat"
* `git reflog` - jako krabička poslední záchrany
* `reflog` je jako zásobník změn
* pokud něco odstraním/ztratím na 99 % to tu najdu
* výchozí cache je 90 dní

--

### Reflog, stash a blame

#### Stash

* rychlé odkladiště
* `git stash` - uloží "stranou" soubory, které se změnily
* `git stash list` - zobrazí seznam změn ve stashi
* `git stash pop` - ostraní poslední revizi ze stashe a aplikuje
* je dobré používat parametr `-m` jinak zapomenete, co ve stashi je

--

### Reflog, stash a blame

#### Blame

* `git blame foo.py` - zobrazí poslední revizi, která změnila každý řádek souboru
* odhalí "viníka" poslední změny na daném řádku

<img src="http://cdn.meme.am/instances/500x/57567283.jpg" width="350">

--

### Konfig a aliasy

#### Konfig

* globální konfigurace - `~/.gitconfig`
* lokální konfigurace - `můj-projekt/.git/config`
* nastavení v souboru nebo příkazem `git config`
* lokální konfigurace přepisuje globální

--

### Konfig a aliasy

#### Konfig - globální

![Git config global](img/git-config-global.png)

--

### Konfig a aliasy

#### Konfig - lokální

![Git config local](img/git-config-local.png)

--

### Konfig a aliasy

#### Aliasy - zkratky pro často používané příkazy

* psát `git checkout` je otravné - `git co`
* nastavení typicky v globální konfiguraci
* příklady

![Git alias](img/git-alias.png)

--

### Další praktické vychytávky

#### .gitignore

* deklarace souborů, které má GIT ignorovat (globální a lokální)
* podporad wildcards
* `*.swp` - ignoruje všechny soubory s příponou `swp`
* typické pro soubory IDE, build složky apod.
* "super-lokální" gitignore - `.git/info/exclude`

--

### Další praktické vychytávky

#### Prázdná složka

* GIT sleduje pouze soubory a proto prázdné složky ignoruje
* pro přidání prázdné složky je nutné ve složce vytvořit prázdný soubor `.gitkeep`

--

### Další praktické vychytávky

#### Odstranění souborů

* `git rm <název-souboru>`
* odstranění souborů připravených ke commitu `git rm --cached <název-souboru>`
* pokud se bojíte, zkuste nejdřív `git rm --dry-run <název-souboru>`

--

### Další praktické vychytávky

#### Odstranění větví

* `git branch --merged` - vypíše mergnuté větve vůči `HEAD`
* `git branch -d <název-větve>` - odstraní danou větev, pouze pokud byla mergnuté do `HEAD`
* `git branch -D <název-větve>` - odstraní danou větev a nic nekontroluje!

--

### Další praktické vychytávky

#### Odstranění vzdálených větví

* `git push public :<název-větve>` - odstraní větev z `public` repozitáře
* nebo `git push --prune public` - odstraní vzdálené větve, pokud nejsou v lokálním repozitáři

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
