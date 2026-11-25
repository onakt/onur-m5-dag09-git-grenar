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
(klistra in)
```

Fråga: Vad betyder `<<<<<<< HEAD`, `=======` och `>>>>>>> grennamn`?


Hur löste du den, och varför blev det så?


## 4. Ångra
Vad är skillnaden mellan `git restore`, `git revert` och `git reset`? Vilken är säkrast när ändringen redan är pushad?


## 5. Pull request
Länk till din pull request (på ditt eget repo):


## 6. Reflektion
Vad är det värsta som kan hända om man kör `git push --force` på en gren som andra använder?


