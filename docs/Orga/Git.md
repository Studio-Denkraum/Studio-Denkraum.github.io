### Branches

Branch| Beschreibung
--- | :--- 
dev | Darauf wird entwickelt und die Feature/Fix-Branches per Pull Request gepushed
main | Beinhaltet einen stabilen Stand des Projekts, darauf wird ein Pull Request nach gemeinsamer Absprache gemacht

### Workflow

Vom Develop-Branch abstammend einen neuen Branch für Feature / Bugfix erstellen. Auf diesem wird gearbeitet und die Arbeit regelmäßig gepushed, bis es fertig ist. Im Anschluss wird ein Pull Request erstellt, um die Änderungen auf dem temporären Branch in Develop zu mergen. Pull Requests können mit GitHub Desktop oder auch direkt auf GitHub.com erstellt werden. Letzteres hat den Vorteil, dass immer mit der aktuellen Version von "dev" gemerged wird. Sonst muss man sichergehen, dass man die aktuellste Version bei sich lokal hat.

[Empfohlender Weg über GitHub.com](https://docs.github.com/de/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) 

Im Pull Request bietet es sich an, eine kurze Beschreibung hinzuzufügen, die die Änderungen zusammenfasst. Gegebenfalls können Dokumente und Bilder angehängt werden. Nach dem Erstellen des Pull Requests auf develop, kann dieser direkt angenommen werden. Es wird kein Approval benötigt. 

### Neuer Remote

Wegen des Repo-Umzugs in die Organisation, muss der Remote bei jeder Person, die bereits mit dem Repo arbeitet, einmalig angepasst werden:

Aktuellen Remote anzeigen:
```
$ git remote -v
origin  git@github.com:Androx765/Game_dev.git (fetch)
origin  git@github.com:Androx765/Game_dev.git (push)
```
Neuen URL als Remote setzen: 
```
git remote set-url origin git@github.com:Studio-Denkraum/game-dev.git
```
Prüfen, ob es geklappt hat:
``` 
$ git remote -v
origin  git@github.com:Studio-Denkraum/game-dev.git (fetch)
origin  git@github.com:Studio-Denkraum/game-dev.git (push)
```
### Namenskonvention

- Feature-Branch: "feature/[beschreibung]"
- Bugfix-Branch: "bugfix/[beschreibung]"
- Hotfix-Branch: "hotfix/[beschreibung]"

Beschreibungen und Branch-Namen generell in **kebab-case**: kleingeschrieben und Worte mit Bindestrich verbunden
-> Zum Beispiel "feature/enemy-movement"

Quelle: https://dev.to/couchcamote/git-branching-name-convention-cch
