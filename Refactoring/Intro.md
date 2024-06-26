# Refactoring

Refactoring is het slim opschonen van je code zonder dat dit iets verandert aan hoe het programma werkt. Het idee is om
de code makkelijker te maken om te lezen en te onderhouden. Dit komt goed van pas als je bijvoorbeeld bugs probeert te
vinden of nieuwe features wilt toevoegen zonder hoofdpijn te krijgen!

We doen aan refactoring omdat het de code netjes houdt. Dit maakt het niet alleen makkelijker voor jou en je team om
snel te begrijpen wat er gebeurt, maar het helpt ook om sneller nieuwe mensen in te werken. Plus, het houdt je codebase
flexibel, waardoor aanpassingen in de toekomst een stuk minder pijnlijk zijn. Dus, een beetje tijd besteden aan
refactoring nu kan je een hoop tijd en moeite besparen later!

**Hier zijn enkele kernrichtlijnen om te volgen:**

**Korte Methoden:** Streef ernaar om methoden niet langer te maken dan ongeveer 10 regels. Korte methoden zijn
makkelijker te lezen, te testen en te debuggen.

**Beperk Nesting:** Probeer niet meer dan twee niveaus van indentatie per methode te hebben. Dit maakt je code minder
complex en gemakkelijker te volgen.

**Juiste Naamgeving:** Geef methoden, variabelen en klassen namen die hun doel duidelijk beschrijven. Vermijd algemene
namen zoals data of info en kies namen die de intentie weergeven, zoals customerAddress of saveEmployeeRecord.

**Eén Taak Per Methode:** Zorg ervoor dat elke methode slechts één ding doet. Dit maakt ze herbruikbaar en makkelijker
te onderhouden.

**Vermijd Magische Getallen en Strings:** Gebruik benoemde constanten voor waarden die betekenis hebben binnen de code,
zoals configuratiewaarden of specifieke limieten.

Deze praktijken helpen bij het creëren van een codebasis die niet alleen functioneel is maar ook aanpasbaar en
toekomstbestendig.