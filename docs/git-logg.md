# Git-logg

Klistra in utskrifter och svara på frågorna. Det här är din dokumentation av dagens arbete.

## 1. Utgångsläget
Skriv ut `git log --oneline --graph --all` direkt efter att du klonat. Klistra in här:

```
* 5a5841d (HEAD -> main, origin/main, origin/HEAD) Modul 5 i TypeScript med Vite
* 3804533 Add files via upload
* f7a13a4 Add files via upload
* c9a0075 Initial commit
```

## 2. Merge utan konflikt
Klistra in `git log --oneline --graph --all` efter merge:

```
*   f743de3 (HEAD -> main) Merge branch 'meny-nyheter'
|\  
| * 0bec895 (meny-nyheter) Steg 2: Lägg till en pizza på menyn
* | 21d4ee3 Steg 3: Lägg till telefonnummer
|/  
* 8568966 Steg 1: Klona och titta runt. Skriv ut en log för utgångsläget
* 5a5841d (origin/main, origin/HEAD) Modul 5 i TypeScript med Vite
* 3804533 Add files via upload
* f7a13a4 Add files via upload
* c9a0075 Initial commit
```

Fråga: Vad är skillnaden mellan en *fast-forward*-merge och en merge som skapar en egen merge-commit? Svara med egna ord: *fast-forward*-merge har main inte fått nya commits sedan grenen skapades, så main flyttas bara fram. Historiken blir en rak linje. Merge-commit sker eftersom båda spåren har fått nya commits. Då sammanförs ändringarna och spåren möts i historiken (visas som en romb).


## 3. Konflikten
Klistra in filen med konfliktmarkörerna, precis som den såg ut innan du löste den:

```
<<<<<<< HEAD
Helger: 10–17
=======
Helger: 09–18
>>>>>>> oppettider-sommar
```

Fråga: Vad betyder `<<<<<<< HEAD`, `=======` och `>>>>>>> grennamn`?
`<<<<<<< HEAD`: Början på min version (grenen jag står på).
`=======`: Skiljer de två versionerna åt.
`>>>>>>> grennamn`: Slutet på den andra versionen.

Hur löste du den, och varför blev det så?
Jag klickade på Accept Current Change :D
Den valde då att behålla det som låg mellan `<<<<<<< HEAD` och `=======`. Det blev så eftersom att jag valde att behålla MIN version.

## 4. Ångra
Vad är skillnaden mellan `git restore`, `git revert` och `git reset`? Vilken är säkrast när ändringen redan är pushad?

`git restore`: återställer filen till senaste commit. Tar bort ocommittade ändringar. Ändrar INTE commit-historiken. Kan användas för att ta bort filer från staging med --staged. Använd när du ändrat en fil men vill ångra ändringen.

`git revert`: Ångra en commit! Skapar en ny commit som ångrar en tidigare commit. Behåller den befintliga commit-historiken. Fungerar även när ändringar har pushats. Säker för samarbete, eftersom den inte skriver om historiken. Använd när du vill ångra en commit som redan pushats.

`git reset`: Flyttar tillbaka HEAD, alltså nuvarande branch till en tidigare commit. Tre vanliga varianter: git reset --soft (behåller ändringarna i staged), git reset --mixed (behåller ändringarna men tar bort dom från staging), git reset --hard (tar bort ändringarna HELT från arbetskatalogen och staging). Använd när du vill korrigera lokal commit-historik, innan ändringar har pushats.

**Säkrast när ändring redan är pushad**: git revert! Den skriver inte om historiken. I stället skapas en ny commit som ångrar den tidigare ändringen. Perfekt när flera personer arbetar i samma repo.

## 5. Pull request
Länk till din pull request (på ditt eget repo):


## 6. Reflektion
Vad är det värsta som kan hända om man kör `git push --force` på en gren som andra använder?


