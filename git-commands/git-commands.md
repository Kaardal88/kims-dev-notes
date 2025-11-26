# Git kommandoer

## Oversikt over git kommandoer som ofte er i bruk + noen man kan luke ut når man trenger dem. Random rekkefølge, men starter med de jeg faktisk bruker ofte.

## Starte nytt prosjekt flow

### I powershell

_På min pc vil det alltid være samme location på mappene. Men andre ganger vil man kanskje opprette prosjektmapper på en spesifikk location, da bruker man mkdir + cd_

- git clone _repo url_ <-- Cloner repo og lager prosjektmappe.
- cd _repo url_ <-- Gå inn i mappen som ble opprettet.
- code . <-- Åpner prosjekt i vsCode.

### Lage ny branch

- git switch -c _newBranch_
- git checkout -b _newBranch_ (gamlemåten men funker)

### Push branchen og sett upstream

- git push -u origin _newBranch_

---

### - git add .

Legger til alt i prosjektet.

### - git add <filnavn>

Legger til endringen kun i den aktuelle filen

### - git commit -m "din melding"

Lager en commit med en kort melding på hva du har gjort/endret.

### - git push

Laster opp commiten til remote (branchen du står på).

### - git push -u origin main

Første push når branch ikke finnes.

## Branches

### -git branch

Viser alle branches

### -git branch <navn>

Lager en ny branch

### -git checkout <navn>

Bytter branch (eldre metode)

### -git switch <navn>

Bytter branch (nyere og anbefalt)

### -git switch -c <navn>

Lager og bytter til en ny branch

### -git merge <navn>

Slår sammen branch inn i nåværende

### -git branch -d <navn>

Sletter branch lokalt

## Pull & merge

### -git pull

Henter og slår sammen endringer fra remote

### -git fetch

Henter endringer uten å slå sammen

### -git merge <branch>

Merger branch inn i aktiv branch

## Repository-håndtering

### -git init

Lager et nytt Git-repo i mappen

### -git clone <repo-url>

Laster ned et repo fra GitHub/GitLab osv.

### -git remote -v

Viser koblede remote-repositories

### -git remote add origin <url>

Knytter repoet til en server (f.eks. GitHub)

## Undo / fiksing

### -git log

Viser commit-historikk

### -git log --oneline

Kort historikk

### -git diff

Viser endringer mellom commits/arbeidsområde

### -git reset --soft <commit>

Går tilbake, men beholder endringer i staging

### -git reset --hard <commit>

Går tilbake og sletter alle endringer (forsiktig!)

### -git revert <commit>

Lager ny commit som “undoer” en gammel commit

## Pull & merge

### -git pull

Henter og slår sammen endringer fra remote

### -git fetch

Henter endringer uten å slå sammen

### -git merge <branch>

Merger branch inn i aktiv branch

## Repository-håndtering

### -git init

Lager et nytt Git-repo i mappen

### -git clone <repo-url>

Laster ned et repo fra GitHub/GitLab osv.

### -git remote -v

Viser koblede remote-repositories

### -git remote add origin <url>

Knytter repoet til en server (f.eks. GitHub)
