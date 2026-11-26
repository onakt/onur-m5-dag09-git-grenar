# Dag 9 · Git: grenar, merge och konflikter

*Modul 5, UI/UX & Frontendutveckling (TypeScript), Lexicon IT-Proffs*

## Vad du ska göra idag

Du lär dig använda Git på riktigt: **grenar** för att arbeta utan att störa `main`, **merge** för att slå ihop, att **lösa en konflikt** när två ändringar krockar, att **ångra** säkert och att öppna en **pull request** på ditt eget repo. Du dokumenterar allt i `docs/git-logg.md`.

## Bakgrund

Hittills har du jobbat på en enda gren och bara gått framåt. I verkligheten jobbar flera personer samtidigt, och du själv vill kunna prova något utan att riskera det som fungerar. Därför finns grenar. En merge-konflikt är inget fel, det är Git som säger: "ni har ändrat samma rad, du måste avgöra vilken som ska gälla". Idag skapar vi konflikten med flit, så att den inte är skrämmande när den dyker upp på riktigt. Du arbetar helt själv, på din egen fork.

## Så arbetar du (samma som alltid)

1. **Forka** dagens repo på GitHub (*Fork → Create fork*).
2. **Klona din fork:** *Code → HTTPS → kopiera adressen*. I terminalen (Ctrl+ö i VS Code): `git clone <adressen>`. Öppna den nya mappen i VS Code.
3. **Gör uppgiften.** Spara och kontrollera i webbläsaren och Console (F12) efter varje steg. Gör en commit efter varje avslutat steg: `git add .` och `git commit -m "Beskriv vad du gjorde"`.
4. **Skicka upp** när du är klar: `git push`.
5. **Lämna in i Microsoft Forms.**

Den här dagen jobbar du med grenar. Du pushar fler grenar än `main`, och du öppnar en pull request. Stegen nedan visar exakt hur.

Fastnar du: skriv ner exakt var och vad du försökt (och vilket felmeddelande du fick), och ta det först i nästa handledda pass.

> Idag behövs ingen `npm install`: repot innehåller bara textfiler. I Steg 8 (`.gitignore`) ser du varför `node_modules/` inte ska med i Git. Samma sak gäller dina övriga repon i modulen, där `.gitignore` redan är ifylld.

## Uppgiften steg för steg

### Steg 1. Klona och titta runt

Forka repot, kör `git clone`, öppna mappen i VS Code. Kör `git log --oneline --graph --all`, `git branch -a` och `git status`. Klistra in loggen i `docs/git-logg.md` (avsnitt 1). Läs igenom `docs/git-fusklapp.md`.

### Steg 2. En gren för en ny funktion

Skapa en gren: `git switch -c meny-nyheter`. Lägg till en rad sist i `kafe-info/meny.md`, till exempel `- Kanelbulle, 33 kr`. Gör `git add .` och `git commit -m "Lägg till kanelbulle på menyn"`. Kör `git branch` och se att du står på grenen. Titta i `kafe-info/meny.md` på `main`: byt med `git switch main` och se att raden inte finns där. Byt tillbaka och se att den finns.

### Steg 3. Merge utan konflikt

Stå på `main`: `git switch main`. Ändra `kafe-info/kontakt.md` (lägg till en rad med ett telefonnummer), `git add .` och `git commit -m "Lägg till telefonnummer"`. Slå ihop: `git merge meny-nyheter`. Editorn öppnas för merge-meddelandet: spara och stäng. Kör `git log --oneline --graph --all` och klistra in grafen i `docs/git-logg.md` (avsnitt 2). Besvara frågan om fast-forward.

### Steg 4. Skapa en konflikt med flit

Skapa två grenar från `main` som ändrar SAMMA rad. Gren 1: `git switch -c oppettider-helg`, ändra `Helger: 09–16` till `Helger: 10–17` i `kafe-info/oppettider.md`, commit. Tillbaka: `git switch main`. Gren 2: `git switch -c oppettider-sommar`, ändra samma rad till `Helger: 09–18`, commit. Tillbaka: `git switch main`. Kör `git merge oppettider-helg` (går bra, en så kallad *fast-forward*). Kör sedan `git merge oppettider-sommar`. Nu får du CONFLICT.

### Steg 5. Lös konflikten

Öppna `kafe-info/oppettider.md` i VS Code. Klistra in filen med markörerna i `docs/git-logg.md` (avsnitt 3) innan du ändrar något. Välj en av raderna, eller skriv en ny (till exempel `Helger: 10–18`), och ta bort ALLA tre markörrader (`<<<<<<<`, `=======`, `>>>>>>>`). Spara. `git add kafe-info/oppettider.md`, sedan `git commit` (spara standardmeddelandet). Kontrollera: `git status` ska vara rent och `git grep "<<<<<<<"` ska inte ge någon träff. Förklara i loggen vad markörerna betyder och hur du valde.

### Steg 6. Avbryt en merge

Skapa en ny konflikt på samma sätt (två nya grenar som ändrar `Röda dagar: stängt` på varsitt sätt). Kör `git merge` så att du får konflikt, och avbryt sedan med `git merge --abort`. Kör `git status`: allt är som förut. Att kunna backa är det som gör konflikter ofarliga.

### Steg 7. Ångra säkert

Ändra något i `kafe-info/meny.md` utan att committa och kör `git restore kafe-info/meny.md` (ändringen försvinner). Gör en commit med en onödig ändring, hitta hashen med `git log --oneline` och kör `git revert <hash>`: Git skapar en ny commit som tar bort effekten, och historiken bevaras. Läs om `git reset --hard` och `git push --force` i fusklappen. Skriv i loggen (avsnitt 4) vilken som är säkrast när något redan är pushat.

### Steg 8. Ignorera filer med .gitignore

Skapa filerna `.env`, `debug.log` och `node_modules/x.txt` (mappen får du skapa själv). Kör `git status`: de syns. Skapa `.gitignore` med raderna `.env`, `*.log` och `node_modules/`. Kör `git status` igen: nu syns bara `.gitignore`. Commit. Förklara varför man aldrig ska committa en `.env`.

### Steg 9. Pull request på ditt eget repo

Skapa en gren `info-uppdatering`, ändra något i `kafe-info/`, committa och kör `git push -u origin info-uppdatering`. På GitHub: *Compare & pull request*. VIKTIGT: ändra *base repository* till ditt EGET repo (som standard föreslår GitHub Lexicon-RC, och det vill du inte). Skriv en beskrivning, klicka *Create pull request* och sedan *Merge pull request*. Lokalt: `git switch main`, `git pull`, `git branch -d info-uppdatering`. Klistra in länken i loggen (avsnitt 5).

### Steg 10. Fördjupning (frivillig): stash och cherry-pick

Läs om `git stash` (lägg undan ändringar tillfälligt) och `git cherry-pick` (plocka en enskild commit till en annan gren). Prova båda i en testgren och förklara när du skulle behöva dem.

## Kontrollista: så vet du att du är klar

- [ ] `docs/git-logg.md` är ifylld med graf-utskrifter, konfliktfilen, förklaringar med egna ord och PR-länk.
- [ ] Historiken innehåller minst en merge-commit och en löst konflikt.
- [ ] Inga konfliktmarkörer finns kvar i någon fil (`git grep "<<<<<<<"` ger inga träffar).
- [ ] Du har avbrutit en merge med `git merge --abort`.
- [ ] Du har en `.gitignore` som döljer `.env`, `*.log` och `node_modules/`.
- [ ] Din pull request är öppnad och mergad på ditt eget repo (inte på Lexicon-RC).
- [ ] Du kan förklara skillnaden mellan `restore`, `revert` och `reset`.

## Tips om du fastnar

- Osäker på var du står? `git status` och `git branch` svarar alltid.
- Konflikt och panik? `git merge --abort` tar dig tillbaka till innan merge.
- Editorn som öppnades fastnar? Skriv ett meddelande, spara och stäng fliken (i VS Code), eller `:wq` i vim.
- Glömde du `git add` efter att ha löst konflikten? `git status` visar "Unmerged paths". Gör `git add filen` och `git commit`.
- Kör aldrig `git reset --hard` eller `git push --force` utan att veta exakt vad de gör. De kan radera arbete.
- Windows-fråga: får du "LF will be replaced by CRLF"? Det är en varning, inte ett fel. Ignorera den.
- Du pushade till fel gren? Kör `git branch` och `git log --oneline --graph --all` och kolla innan du gör något drastiskt.

## Inlämning

**Deadline: imorgon klockan 09.00.** Allt lämnas in i Microsoft Forms. Du behöver inte redovisa något muntligt.

I formuläret fyller du i:

1. Länk till din fork av det här repot.
2. Reflektion: Vad är en merge-konflikt, varför uppstår den, och varför är det okej att den uppstår? Beskriv hur du löste din egen konflikt, steg för steg.

## Vill du mer? (frivilligt)

- Skapa en tredje gren som ändrar samma rad och slå ihop alla tre. Hur ser filen ut mitt i konflikten?
- Läs om `git rebase` och beskriv skillnaden mot `git merge` med egna ord. Kör inte rebase på delade grenar.
- Ställ in grenskydd på `main` i ditt repo på GitHub (Settings, Branches, Add rule) så att man måste använda pull request. Förklara varför team gör så.
