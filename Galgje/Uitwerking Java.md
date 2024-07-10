# Uitwerking Java

Hier is een voorbeeld van een eenvoudig Galgje-spel in Java:

```java
import java.util.Scanner;

public class Galgje {

    // De lijst van woorden waaruit een willekeurig woord wordt gekozen
    private static final String[] WOORDEN = {
        "programmeren", "java", "computer", "spel", "internet",
        "galgje", "software", "hardware", "database", "netwerk"
    };

    // Methode om een willekeurig woord te kiezen uit de lijst van woorden
    private static String kiesWillekeurigWoord() {
        int index = (int) (Math.random() * WOORDEN.length);
        return WOORDEN[index];
    }

    // Methode om te controleren of het geraden woord volledig is geraden
    private static boolean isGeraden(String woord, boolean[] geradenLetters) {
        for (int i = 0; i < woord.length(); i++) {
            if (!geradenLetters[i]) {
                return false;
            }
        }
        return true;
    }

    // Methode om de huidige stand van het woord te printen
    private static void printGalgjeStatus(String woord, boolean[] geradenLetters) {
        for (int i = 0; i < woord.length(); i++) {
            if (geradenLetters[i]) {
                System.out.print(woord.charAt(i) + " ");
            } else {
                System.out.print("_ ");
            }
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String woord = kiesWillekeurigWoord();
        boolean[] geradenLetters = new boolean[woord.length()];
        int pogingen = 6;
        StringBuilder fouteLetters = new StringBuilder();

        System.out.println("Welkom bij het spel Galgje!");

        // Loop totdat het woord volledig is geraden of de pogingen op zijn
        while (pogingen > 0 && !isGeraden(woord, geradenLetters)) {
            System.out.println("\nResterende pogingen: " + pogingen);
            System.out.print("Gok een letter: ");
            char gok = scanner.next().toLowerCase().charAt(0);

            boolean juistGeraden = false;
            for (int i = 0; i < woord.length(); i++) {
                if (woord.charAt(i) == gok && !geradenLetters[i]) {
                    geradenLetters[i] = true;
                    juistGeraden = true;
                }
            }

            if (juistGeraden) {
                System.out.println("Juist! De huidige stand:");
                printGalgjeStatus(woord, geradenLetters);
            } else {
                if (fouteLetters.indexOf(String.valueOf(gok)) == -1) {
                    fouteLetters.append(gok).append(" ");
                    pogingen--;
                }
                System.out.println("Fout! Probeer opnieuw.");
                System.out.println("Foute letters: " + fouteLetters);
                printGalgjeStatus(woord, geradenLetters);
            }
        }

        // Controleer of de speler heeft gewonnen of verloren
        if (isGeraden(woord, geradenLetters)) {
            System.out.println("Gefeliciteerd! Je hebt het woord geraden: " + woord);
        } else {
            System.out.println("Helaas, je hebt verloren. Het woord was: " + woord);
        }

        scanner.close();
    }
}
```

## Toelichting:

- **WOORDEN**: Een array met een aantal woorden waaruit een willekeurig woord wordt gekozen.
- **kiesWillekeurigWoord**: Methode om willekeurig een woord te kiezen.
- **isGeraden**: Methode om te controleren of het hele woord is geraden.
- **printGalgjeStatus**: Methode om de huidige status van het woord weer te geven.
- **main**: De hoofdmethod die het spel logic implementeert.

## Hoe het programma uit te voeren:

1. Kopieer de bovenstaande code naar een bestand genaamd `Galgje.java`.
2. Compileer het programma met `javac Galgje.java`.
3. Voer het programma uit met `java Galgje`.

