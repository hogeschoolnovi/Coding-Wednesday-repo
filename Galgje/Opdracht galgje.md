# Galgje workshop:programmeren

Welkom bij de "Coding Wednesday" Galgje Workshop! In deze sessie leer je hoe je het klassieke spel "Galgje" kunt ontwerpen en implementeren. We zullen het proces doorlopen van de basisregels tot het daadwerkelijk schrijven van de code, terwijl we je voorzien van een plan van aanpak.

### Workshop overzicht
1. **Theorie: Introductie en Regels van Galgje**
   - **Doel:** Begrijp de basisregels van Galgje en het ontwerp van de applicatie.
   - **Regels:**
      - Kies een geheim woord.
      - De speler probeert het woord te raden door letters één voor één te kiezen.
      - Voor elke verkeerde letter wordt een deel van de galg getekend.
      - Als het volledige poppetje is getekend, heeft de speler verloren.
      - De speler wint als het woord volledig is geraden.
   - **Basisimplementatie:**
      - Definieer een lijst van mogelijke woorden.
      - Kies willekeurig een geheim woord.
      - Houd de geraden letters en resterende pogingen bij.

2. **Plan van Aanpak**
   - **Project Structuur:**
      - Kies een programmeertaal naar keuze (bijvoorbeeld Python, Java, C#, etc.).
      - **Belangrijkste Componenten:**
         - Game Loop: De hoofdlogica voor het spel.
         - Woordgeneratie: Functie om een willekeurig woord te selecteren.
         - Input en Output: Invoeren van raden en afdrukken van de huidige status.
         - Win/Loss Logica: Logica voor winst/verlies scenarios.

   **Diagram: Logica Overzicht**
   ```mermaid
   flowchart TD
       Start[Start] --> Initialize[Initialiseer Woordenlijst en Raad Package]
       Initialize --> Select[Selecteer Geheim Woord]
       Select --> Loop[Game Loop: Raden]
       Loop --> Check[Controleer Status]
       Check -->|Geraden| Win[Gefeliciteerd! Je hebt gewonnen!]
       Check -->|Fout| Draw[Update Galgje Status]
       Draw -->|Max Pogingen Bereikt| Lose[Game Over!]
       Draw --> Loop
   ```

3. **Implementatie: Bouw de Basisstructuur**
   - **Hints voor Implementatie in Diverse Talen:**
      - **Kies een Woord:**
         - Python: Gebruik `random.choice()`.
         - JavaScript: Gebruik `Math.random()` in combinatie met array indexering.
         - Java/C#: Gebruik `Random` klasse om een willekeurige index te selecteren uit een array of lijst.
      - **Game Loop:**
         - Zorg voor een loop die blijft draaien totdat het woord is geraden of het maximale aantal pogingen is bereikt.
         - Controleer binnen de loop de ingevoerde letter en update de geraden letters en galg status.
      - **Input en Output:**
         - Python: Gebruik `input()` voor invoer en `print()` voor uitvoer.
         - Java: Gebruik `Scanner` voor invoer en `System.out.println()` voor uitvoer.
         - JavaScript: Gebruik `prompt()` voor invoer (in een browseromgeving) en `console.log()` voor uitvoer.
      - **Win/Loss Logica:**
         - Controleer na elke ronde of het woord volledig is geraden of het maximale aantal pogingen is bereikt om te bepalen of de speler heeft gewonnen of verloren.

4. **Break**

5. **Uitbreiding: Verbetering van de Functies**
   - **Doel:** Voeg extra functionaliteit en betere gebruikerservaring toe.
   - **Mogelijke Verbeteringen:**
      - Gebruik ASCII-art of grafische weergave om het poppetje te tekenen.
      - Zorg voor correcte input door de speler.
      - Voeg meerdere niveaus toe gebaseerd op de lengte van het woord.
      - Houd scores bij voor geraden woorden.

   **Hints voor Uitbreiding:**
   - Maak een array of lijst met verschillende stadia van de galg.
   - Update de weergave na elke verkeerde gok.
   - Controleer of de invoer een enkele letter is en of deze nog niet eerder is geraden.
   - Gebruik de lengte van het woord of een moeilijkheidsrating om de woordenlijst te filteren.
   - Houd een scorebord bij in een bestand of een database.
   - Voeg een naamveld toe voor de speler om zijn/haar score op te slaan.

6. **Eindopdracht: Bouw Galgje in Teams**
   - **Doel:** Werk in teams om een complete versie van Galgje te bouwen.
   - **Plan van Aanpak:**
      - Vorm teams van 3-4 personen.
      - Verdeel de taken zoals UI-ontwerp, woordkeuze, en game-logica.
      - Voeg moeilijkheidsniveaus toe.
      - Voeg een scorebord toe om scores op te slaan.
      - Voeg de optie toe om opnieuw te spelen.

   **Hints voor Scorebord:**
   - **Lezen en Schrijven naar een Bestand:**
   - Python: Gebruik `open()` om bestanden te lezen en schrijven.
   - Java: Gebruik `FileReader` en `FileWriter`.
   - C#: Gebruik `StreamReader` en `StreamWriter`.
   - **Structuur van Scorebord:**
   - Houd een lijst van scores bij en sorteer deze op basis van de hoogste scores.
   - Toon de top scores na elke game.

7. **Afronden**
   - **Reflectie:** Wat waren de uitdagingen? Hoe kun je het spel verder verbeteren?

Veel succes en plezier bij het bouwen van Galgje!