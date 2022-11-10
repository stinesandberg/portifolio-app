# Git

## Forke repository

Når du "Forker" et prosjekt lager du en kopi av repoet til ditt eget prosjekt på din egen github der du kan eksperimentere med endringer uten å påvirke det originale prosjektet.

```
   Gå inn på dette prosjektet i github (pass på at du er pålogget).
   Klikk på Fork-ikonet oppe i hjørnet av denne siden.
   Som standard vil det originale prosjekt-navnet bli foreslått, men gjerne endre det til noe eget.
   Trykk på "Create fork" knappen.
```

## Åpne terminalen

Åpne foretrukket terminal. F.eks Git Bash, Command Prompt, Terminal eller iTerm.

## Forbered mappe hvor koden skal ligge

Lag en mappe i finder der du ønsker at koden skal ligge.
Når mappen er laget, så drar du den inn i terminal-vinduet.
Filstien til mappen vil dukke opp i terminalen. Eks: `C:\Documents\NTNU\` eller `/Users/stinesandberg/Jobb/Ada\ NTNU`
Skriv "cd" foran filstien som har dukket opp. Eks: `cd C:\Documents\NTNU\` eller `cd /Users/stinesandberg/Jobb/Ada\ NTNU`
Trykk Enter, og du er nå inni mappen du lagde.


Dersom det ikke fungerer å dra mappen inn i terminal-vinduet kan du navigere deg frem til den manuelt ved bruk av `cd` og `ls`.
Les dokumentasjonen [her for Mac](https://www.macworld.com/article/221277/command-line-navigating-files-folders-mac-terminal.html) og [her for Windows](https://www.howtogeek.com/659411/how-to-change-directories-in-command-prompt-on-windows-10/).

Dersom du får opp en popup der terminalen vil ha tilgang til feks "filene i skrivebordet ditt", trykk ok.

## Clone repository

`git clone [https link fra github]`

Eks:
`git clone https://github.com/zstinesandbergz/portifolio-app.git`

Du kan nå se i mappen du lagde om kode-filene har kommet inn i mappen.

## Klargjøre opplasting av lokale endringer til Github

Når du har gjort endringer i koden på din maskin, så er disse endringene bare lagret lokalt på din maskin.
For å laste opp endringene dine til Github så må du først definere hvilke av de endrede filene du vil laste opp:

Se hvilke filer som har blitt endret (endrede filer som ikke er klargjort for opplasting vises som røde):
`git status`

Dersom du ønsker å laste opp alle endrede filer kan du bruke følgende kommando (stort sett denne man trenger):
`git add .`

Dersom du ønsker å bare laste opp noen av de endrede filene så kan du bruke denne kommandoen:
`git add [filnavn]`

Eks:
`git add src/index.js`

Deretter kan du sjekke at filene du vil laste opp har blitt klargjort (de skal nå vises som grønne):
`git status`

## Opprette commit med de klargjorte filene

Nå som du har bestemt hvilke filer som skal lastes opp til Github, så må du lage en commit.
Dette er som et log-item/snapshot i git historikken til ditt prosjekt som viser hvilke endringer som har blitt gjort på dette tidspunktet.
Denne trenger en kort beskrivelse av hva som har blitt gjort; en såkalt commit message.

`git commit -m "Du skriver beskjeden din i mellom hermetegnene her"`

Eks:
`git commit -m "Updated the git-guide"`

## Pushe endringene til Github

Det eneste som nå gjenstår er å faktisk sende endringene til Github:

`git push`

Du kan nå gå inn i repositoriet på din bruker på github.com og se at endringene du har gjort i filene ligger der.


## Vanlige feil og hvordan fikse dem


### Permission denied (publickey)
Når du prøver å pushe kan du få feilmelding: 
`Permission denied (publickey)`

Dette er et SSH problem, og kan bety at du har clonet repoet med SSH istedenfor https. 
For å løse problemet har du to valg;
* Clone repoet på nytt ved bruk av https, kopiere over endrede filer i den nye clonede mappen
* Sette opp SSH på mac/windows i terminalen (anbefales ikke ettersom det kan være vanskelig å få til). Du har en guide på hvordan dette gjøres [her](https://www.inmotionhosting.com/support/server/ssh/how-to-add-ssh-keys-to-your-github-account/)



### Tip of your current branch is behind its remote counterpart
Når du prøver å pushe kan du få feilmelding: 

`Updates were rejected because the tip of your current branch is behind its remote counterpart. Integrate the remote changes (e.g. hint: 'git pull ...') before pushing again.`

Dette skjer fordi kodeversjonen som ligger i Github (remote branch) har endringer som du ikke har på din lokale kodeversjon (local branch).
Det kan skje enten ved at det har kommet inn commits på den remote branchen som ikke du har pullet ned, eller at noen har endret historien på remote branch (vanligvis en form for rebase).

⚠️  Dersom du er 100% sikker på at det ikke er noen endringer på remote branch, og at du faktisk har clonet ned riktig repository, så kan du kjøre `git push -f`.  
Dette vil force alle dine lokale endringer opp på remote branch og dermed overskrive eventuelle endringer som ligger på remote branch.


Dersom du derimot er usikker på om det er endringer på remote branch som du vil ha, så prøver du heller å hente ned endringene før du pusher. 
For å hente ned endringene fra remote branch kan du kjøre en:
`git pull`

eller 
`git pull origin [name of branch]`
f.eks: `git pull origin main`


### 403 Error
Hvis du får en eller annen 403 error betyr det at du ikke er autentisert. 


Dersom du får opp at du må skrive inn brukernavn og passord i terminalen når du prøver å kjøre en git push så vil brukernavnet være github brukernavnet deres, og passordet vil være en Personal Access Token. 
Du må derfor inn på Github kontoen din i browseren og generere en Personal Access Token. Dette gjøres ved å trykke på profilbildet i hjørnet -> Settings -> Developer Settings (helt nederst i menyen på venstre side) -> Personal Access Tokens -> Tokens (classic) -> Generate new token
Når du lager en ny token må du passe på at du krysser av på at du skal ha alle rettigheter på alt. 


Om du ikke får opp at du må skrive inn brukernavn og passord, så må du først sette hva slags autentiseringsmetode som skal brukes: 
`git remote set-url origin [samme https link du bruker for å clone prosjektet]`

Og når du så kjører `git push` så skal det dukke opp en promt til å skrive inn brukernavn og passord. Du bruker da fremgangsmåten over med github brukernavn og Personal Access Token.


### Fatal: Not a git Repository (or any of the parent directories)
En annen vanlig feil er at man er inne i en mappe som ikke har en generert .git fil. Dersom du har clonet et repo fra github(hvilket du skal ha gjort i dette prosjektet) så er .git filen allerede generert for deg, og denne feilen tyder da på at du ikke er i riktig directory i terminalen.

Bruk `cd [filsti til repositoriet på maskinen din]` for å komme inn i riktig mappe.  


### Ressursser for feilsøking
[Mest vanlige feilmeldinger i git og hvordan fikse dem](https://betterprogramming.pub/common-git-errors-2e379516dc65)
