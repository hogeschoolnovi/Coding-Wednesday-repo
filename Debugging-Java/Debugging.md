# Debugging challenge

In deze sessie leer je effectief bugs opsporen en oplossen met
behulp van de debugger in IntelliJ IDEA. Ontdek wat breakpoints zijn, hoe je variabelen kunt inspecteren en analyseer
waar fouten zich bevinden.

## Workshop overzicht

**Inleidende Theorie**

- **Wat zijn breakpoints en hoe gebruik je ze?**
    - Breakpoints zijn punten in de code waar je de uitvoering kunt pauzeren om de staat van het programma te
      inspecteren.
- **Hoe gebruik je de debugger tools in IntelliJ:**
    - Variabelen inspecteren: Bekijk de waarden van variabelen tijdens het debuggen.
    - Watches toevoegen: Houd bepaalde variabelen in de gaten.
    - Call Stack inspectie: Analyseer de volgorde van methodenaanroepen.
    - Expressions evalueren: Voer uitdrukkingen uit tijdens het debuggen om de uitkomsten te controleren.
    - **Navigeren in de debugger:**
        - *Step Over*, *Step Into*, *Step Out*, *Resume*: Verschillende manieren om door de code te navigeren tijdens
          het debuggen.


### **Oefening 1: Debuggen van datum- en tijdwaarden met UTC**

**Doel:** Ontdek het verschil tussen de verwachte en werkelijke uitvoer door het gebruik van UTC-tijd. Gebruik watches om de datum- en tijdvariabelen te inspecteren en te begrijpen waarom de uitvoer afwijkt.

**Code Voorbeeld:**

```java
import java.util.Calendar;
import java.util.TimeZone;

public class DateTimeDebugExample {
    public static void main(String[] args) {
        // Stel de tijdzone in op UTC
        Calendar calendar = Calendar.getInstance(TimeZone.getTimeZone("UTC"));
        int dag = calendar.get(Calendar.DAY_OF_MONTH);
        int maand = calendar.get(Calendar.MONTH); 
        int jaar = calendar.get(Calendar.YEAR);
        int uur = calendar.get(Calendar.HOUR_OF_DAY);
        int minuut = calendar.get(Calendar.MINUTE);
        int seconde = calendar.get(Calendar.SECOND);

        printDateTime(dag, maand, jaar, uur, minuut, seconde);
    }

    private static void printDateTime(int dag, int maand, int jaar, int uur, int minuut, int seconde) {
        System.out.println("Datum en tijd in UTC: " + dag + "/" + maand + "/" + jaar + " " + uur + ":" + minuut + ":" + seconde);
    }
}
```

**Stappenplan:**

1. **Zet een breakpoint** op regel `20` (`System.out.println(...)`) in de `printDateTime`-methode.
2. **Start de debugger** en laat de code tot het breakpoint lopen.
3. **Maak watches** aan voor de variabelen `dag`, `maand`, `jaar`, `uur`, `minuut`, en `seconde`. Deze variabelen worden in de `main`-methode gedeclareerd en worden doorgegeven aan de `printDateTime`-methode.
4. **Vergelijk de verwachte tijd met de werkelijke tijd** die wordt uitgeprint. Denk hierbij aan de tijdzoneverschillen.
5. **Reflecteer** op waarom de uitgeprinte tijd in UTC verschilt van de lokale tijd op je computer.

**Extra Tip:**
- Voeg ook een watch toe voor `calendar.getTimeZone().getID()` om te zien welke tijdzone daadwerkelijk wordt gebruikt.
- Probeer te begrijpen hoe het werken met verschillende tijdzones van invloed is op de datum- en tijdwaarden.

**Oplossing:**
<details>
<summary>Klik hier voor de uitleg</summary>

De uitgeprinte datum en tijd zijn gebaseerd op de UTC-tijdzone. Dit kan verschillen van de lokale tijd op je computer, vooral als je in een andere tijdzone werkt. Dit verschil is essentieel om te begrijpen bij het werken met systemen die wereldwijd worden gebruikt.

De Calendar.MONTH gebruikt een null teller. Dus Jan is maand 0, je zou dus eigenlijk er een maand bij op moeten tellen.

```
int maand = calendar.get(Calendar.MONTH) + 1; // Maanden zijn 0-gebaseerd in Calendar
```

### **Oefening 2: Debuggen met Step Over en Step Into**

**Doel:** Leer het verschil tussen "Step Over" en "Step Into" door methodes te debuggen en te begrijpen hoe de control flow van een programma werkt.

**Code Voorbeeld:**

```java
public class DebuggingExample {
    public static void main(String[] args) {
        int a = 5;
        int b = 10;

        int result1 = multiply(a, b);
        int result2 = add(result1, 20);
        int result3 = subtract(result2, 15);

        printResult(result3);
    }

    private static int multiply(int x, int y) {
        return x * y;
    }

    private static int add(int x, int y) {
        return x + y;
    }

    private static int subtract(int x, int y) {
        return x - y;
    }

    private static void printResult(int result) {
        System.out.println("Final result: " + result);
    }
}
```

**Stappenplan:**

1. **Zet een breakpoint** op de eerste regel van de `main`-methode (`int a = 5;`).
2. **Start de debugger** en laat de code stoppen bij het breakpoint.
3. **Gebruik "Step Over"** om door de variabelen `a` en `b` te stappen.
4. **Gebruik "Step Into"** bij de aanroep van `multiply(a, b)` om de `multiply`-methode in te gaan.
    - Observeer hoe de control flow van het programma naar de `multiply`-methode gaat.
5. **Gebruik "Step Over"** om door de rest van de statements in de `multiply`-methode te stappen.
    - Let op hoe je door de methode kunt stappen zonder de interne details te hoeven zien.
6. **Gebruik "Step Into"** bij de aanroep van `add(result1, 20)` om te begrijpen hoe deze methode werkt.
    - Observeer de flow van `add` en begrijp het verschil met `multiply`.
7. **Gebruik "Step Over"** bij de aanroep van `subtract(result2, 15)` om door de code te stappen zonder de methode in te gaan.
    - Begrijp wanneer je "Step Over" gebruikt om tijd te besparen of wanneer de interne details van de methode minder belangrijk zijn.
8. **Gebruik "Step Into"** bij de aanroep van `printResult(result3)` om te zien hoe het resultaat wordt geprint.

**Reflectie:**

- **Step Over:** Wordt gebruikt wanneer je een methode wilt uitvoeren zonder de details van die methode in te zien. Dit is handig wanneer je de interne werking van de methode al kent of wanneer je snel door eenvoudige methodes wilt gaan.

- **Step Into:** Wordt gebruikt wanneer je de details van een methode wilt onderzoeken. Dit is handig wanneer je wilt begrijpen hoe de methode werkt of wanneer je op zoek bent naar mogelijke fouten binnen die methode.

**Oplossing:**
<details>
<summary>Klik hier voor de reflectie</summary>

Tijdens het debuggen met "Step Into" zul je zien hoe de programmaflow van de ene methode naar de andere springt. Dit geeft je inzicht in de sequentie waarin methodes worden uitgevoerd en hoe variabelen door de methodes worden gepasseerd. Met "Step Over" kun je efficiënt door de code navigeren wanneer je niet geïnteresseerd bent in de details van een methode.

**Samenvatting van de control flow:**
1. `multiply(a, b)` voert de vermenigvuldiging uit.
2. `add(result1, 20)` voert de optelling uit.
3. `subtract(result2, 15)` voert de aftrekking uit.
4. `printResult(result3)` print het uiteindelijke resultaat.

Door deze oefening te voltooien, zul je een beter begrip hebben van wanneer je "Step Over" en "Step Into" moet gebruiken tijdens het debuggen.
</details>


### **Oefening 3: Onderzoek een stacktrace en plaats een breakpoint**

**Doel:** Leer hoe je een stacktrace analyseert om de oorzaak van een fout te vinden, en hoe je een breakpoint op de juiste plaats zet om de fout te onderzoeken.

**Code Voorbeeld:**

```java
public class StackTraceExample {
    public static void main(String[] args) {
        try {
            processInput("123");
            processInput("abc");  
            processInput("456");
        } catch (NumberFormatException e) {
            System.out.println("Er is een fout opgetreden: " + e.getMessage());
            e.printStackTrace();
        }
    }

    private static void processInput(String input) {
        int number = convertToInt(input);
        System.out.println("Verwerkte waarde: " + number);
    }

    private static int convertToInt(String input) {
        return Integer.parseInt(input);  // Dit kan een NumberFormatException veroorzaken
    }
}
```

**Stappenplan:**

1. **Voer de code uit** zonder de debugger. De code zal een fout veroorzaken wanneer geprobeerd wordt de string `"abc"` om te zetten naar een integer.
2. **Bekijk de stacktrace** die wordt uitgeprint wanneer de `NumberFormatException` optreedt.
    - De stacktrace toont de exacte plaats in de code waar de fout is opgetreden, samen met de methodes die zijn aangeroepen tot dat punt.
3. **Analyseer de stacktrace** om te bepalen in welke methode de fout is opgetreden. Let op de regels in de stacktrace die verwijzen naar jouw codebestanden en methoden.
4. **Plaats een breakpoint** in de methode waar de fout optreedt, zoals aangegeven door de stacktrace. In dit geval zal dit waarschijnlijk de regel zijn waar `Integer.parseInt(input)` wordt aangeroepen in de `convertToInt`-methode.
5. **Start de debugger** en laat de code opnieuw uitvoeren, maar nu met het breakpoint actief.
6. **Stap door de code** vanaf het breakpoint om te begrijpen hoe de input `"abc"` leidt tot de `NumberFormatException`.
    - Gebruik hierbij "Step Over" om door de statements te stappen en "Step Into" om methodes verder te onderzoeken als dat nodig is.
7. **Inspecteer de variabelen** om te zien waarom de conversie mislukt. In dit geval kun je bijvoorbeeld bekijken wat de waarde van `input` is op het moment dat de fout optreedt.
8. **Bedenk een oplossing** om de fout te voorkomen. Dit kan bijvoorbeeld het toevoegen van een validatie zijn voordat je de string probeert om te zetten naar een integer.

**Oplossing:**
<details>
<summary>Klik hier voor de uitwerking</summary>

**Analyse van de stacktrace:**
- De stacktrace laat zien dat de fout optreedt in de `convertToInt`-methode op de regel waar `Integer.parseInt(input)` wordt aangeroepen.
- De stacktrace vermeldt de methode-aanroep keten: `main -> processInput -> convertToInt`.

**Oplossing in de code:**

Een mogelijke manier om de fout te voorkomen is door de input te valideren voordat je de conversie uitvoert:

```java
private static int convertToInt(String input) {
    try {
        return Integer.parseInt(input);
    } catch (NumberFormatException e) {
        System.out.println("Ongeldige invoer voor conversie: " + input);
        return 0;  // Of een andere passende waarde of actie
    }
}
```




### **Oefening 5: Debuggen met een conditional Breakpoint**

**Doel:** Leer hoe je een conditional breakpoint instelt om een fout in een geneste loop op te sporen. In deze oefening wordt de fout veroorzaakt door een subtiele combinatie van variabelen, waardoor het minder duidelijk is waar de fout precies optreedt.

**Scenario:**
Je hebt een programma dat een geneste loop gebruikt om combinaties van elementen uit twee lijsten te verwerken. Onder bepaalde voorwaarden wordt er een fout gegenereerd, maar het is niet meteen duidelijk waar en waarom dit gebeurt. Je moet de fout opsporen door de juiste conditie voor het breakpoint in te stellen.

**Code Voorbeeld:**

```java
import java.util.Arrays;
import java.util.List;

public class ConditionalBreakpointExample {
    public static void main(String[] args) {
        List<Integer> list1 = Arrays.asList(1, 2, 3, 4, 5);
        List<Integer> list2 = Arrays.asList(10, -5, 3, 0, 8);

        try {
            processLists(list1, list2);
        } catch (Exception e) {
            System.out.println("Er is een fout opgetreden: " + e.getMessage());
            e.printStackTrace();
        }
    }

    private static void processLists(List<Integer> list1, List<Integer> list2) {
        for (int i = 0; i < list1.size(); i++) {
            for (int j = 0; j < list2.size(); j++) {
                int result = calculateResult(list1.get(i), list2.get(j));
                System.out.println("Resultaat voor combinatie " + list1.get(i) + " en " + list2.get(j) + " is: " + result);
            }
        }
    }

    private static int calculateResult(int a, int b) {
        int intermediate = a * b;  // Kan leiden tot overflow
        int result = 100 / (intermediate % 7);  // Mogelijke divisie door nul of negatieve waarde
        return result;
    }
}
```

**Stappenplan:**

1. **Voer de code uit** zonder de debugger. Je zult merken dat de code op een bepaald moment een fout gooit, maar het is niet direct duidelijk waarom.

2. **Bekijk de stacktrace** die wordt uitgeprint wanneer de fout optreedt.
    - Analyseer de stacktrace om te bepalen in welke methode en op welke regel de fout plaatsvindt. Noteer de betrokken methodes en regels.

3. **Zet een conditional breakpoint** in de `calculateResult`-methode op de regel waar `100 / (intermediate % 7)` plaatsvindt.
    - Stel de conditie in om te stoppen wanneer `intermediate % 7 == 0` of `intermediate % 7 < 0`. Dit zijn de situaties waarin de fout kan optreden (deling door nul of onverwachte negatieve waarde).

4. **Start de debugger** en laat de code uitvoeren. De debugger zal nu alleen stoppen wanneer de conditie van het breakpoint waar is (d.w.z., wanneer `intermediate % 7` gelijk is aan 0 of negatief).

5. **Gebruik "Step Over"** om door de statements te stappen zodra het breakpoint is bereikt.
    - Inspecteer de waarden van `a`, `b`, `intermediate`, en het uiteindelijke `result` om te begrijpen waarom de fout optreedt.

6. **Bedenk een oplossing** om de fout te corrigeren. Je zou bijvoorbeeld kunnen controleren of de waarde van `intermediate % 7` geldig is voordat je de deling uitvoert.

7. **Implementeer de oplossing** en voer de code opnieuw uit met de debugger om te bevestigen dat de fout is opgelost.

**Oplossing:**
<details>
<summary>Klik hier voor de uitwerking</summary>

**Aanpassingen in de code:**

Je kunt de deling beveiligen door eerst te controleren of de waarde van `intermediate % 7` geldig is:

```java
private static int calculateResult(int a, int b) {
    int intermediate = a * b;
    if (intermediate % 7 == 0) {
        System.out.println("Kan niet delen door 0 voor combinatie " + a + " en " + b);
        return 0;  // Of een andere passende actie, zoals het negeren van de berekening
    }
    int result = 100 / (intermediate % 7);
    return result;
}
```

**Reflectie:**
- **Conditional Breakpoint:** Door een conditional breakpoint in te stellen, kun je de fout isoleren zonder door alle iteraties te stappen. Dit is vooral nuttig in situaties waarin de fout alleen onder specifieke omstandigheden optreedt.
- **Oplossen van de fout:** Door een if-statement toe te voegen, kun je ervoor zorgen dat de foutieve situatie wordt afgehandeld voordat de deling plaatsvindt.

Deze oefening leert je hoe je gericht kunt debuggen en hoe je subtiele fouten kunt opsporen en oplossen.
</details>







**Fun challenge - Kraak de kluis**

- wie kan als eerste het geheime woord vinden?

Pas de toegangscodes aan om toegang te krijgen tot het geheime woord. Gebruik je kennis van debuggen om de codes te vinden

````java
class DebugSafe {

    private static int startChar = 'A';
    private static int endChar = 'z';


    public static void main(String[] args) {
        int code1 = 0 ;
        String code2 = "";
        String code3 = "";

        if (checkCode1(code1) && checkCode2(code2) && checkCode3(code3)) {
            revealSecretWord(code3, code2, code1);
        } else {
            System.out.println("Niet alle codes zijn correct. Probeer het opnieuw.");
        }
    }

    public static boolean checkCode1(int code1) {
        int[] numbers = {1000171, 1000172, 1000173, 1000174};
        for (int number : numbers) {
            if (number == code1 && code1 % 10 == 3) {
                return true;
            }
        }
        return false;
    }


    public static boolean checkCode2(String code2) {
        if (code2.length() != 5) {
            return false;
        }
        for (int i = 0; i < code2.length(); i++) {
            char c = code2.charAt(i);
            var charCorrect =false;
            if(i % 2 == 0 ) {
                charCorrect = checkUpperCase(c) && checkStartCharPlusIndex(i, c);
            }
            else  {
                charCorrect =  checkLowerCase(c) && checkEndcharMinusIndex(i,c);
            }
            if (charCorrect == false) {
                return false;
            }
        }
        return true;
    }

    private static boolean checkLowerCase(char c) {
        return Character.isLowerCase(c);
    }

    private static boolean checkEndcharMinusIndex(int i, char c) {
        return c ==  (char)((endChar-i));
    }

    private static boolean checkStartCharPlusIndex(int i, char c) {
        return c ==  (char)((startChar+i));
    }

    private static boolean checkUpperCase(char c) {
        return Character.isUpperCase(c);
    }

    public static boolean checkCode3(String code3) {
        if (code3.length() != 5) {
            return false;
        }
        for (int i = 0; i < code3.length(); i++) {
            char c = code3.charAt(i);
            if (!checkStartCharPlusIndex(i,c)) {
                return false;
            }
        }
        return true;
    }

    public static void revealSecretWord(String code1, String code2, int code3) {
        int shift1 = code1.charAt(0) - 'A';
        int shift2 = code2.charAt(4) - 'V';
        int shift3 = code3;
        int totalShift = (shift1 + shift2 + shift3) % 26;

        String encryptedWord = "Vcsfo vsh wg qcrwbu ksrbsgrom!";
        String decryptedWord = decrypt(encryptedWord, totalShift);
        System.out.println("Geheim woord: " + decryptedWord);
    }

    public static String decrypt(String text, int shift) {
        StringBuilder result = new StringBuilder();
        for (char c : text.toCharArray()) {
            if (Character.isLetter(c)) {
                char shifted = (char) (c - shift);
                if (c >= 'a' && c <= 'z' && shifted < 'a') {
                    shifted += 26;
                } else if (c >= 'A' && c <= 'Z' && shifted < 'A') {
                    shifted += 26;
                }
                result.append(shifted);
            } else {
                result.append(c);
            }
        }
        return result.toString();
    }

    public static String encrypt(String text, int shift) {
        StringBuilder result = new StringBuilder();
        for (char c : text.toCharArray()) {
            if (Character.isLetter(c)) {
                char shifted = (char) (c + shift);
                if (c >= 'a' && c <= 'z' && shifted > 'z') {
                    shifted -= 26;
                } else if (c >= 'A' && c <= 'Z' && shifted > 'Z') {
                    shifted -= 26;
                }
                result.append(shifted);
            } else {
                result.append(c);
            }
        }
        return result.toString();
    }
}
````
**SUCCES !!!**

## Nuttige links en documentatie

- [Debugger Basics in IntelliJ IDEA](https://www.jetbrains.com/help/idea/debugging-your-first-java-application.html)
- [Breakpoints in IntelliJ IDEA](https://www.jetbrains.com/help/idea/using-breakpoints.html)

Veel succes met de debugging challenge en leer vooral veel!