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

**Oefening 1: NullPointerException**

**Doel:** Ontdek waarom de fout optreedt en corrigeer deze.

**Code Voorbeeld:**

   ```java
   public class NullPointerExample {
    public static void main(String[] args) {
        String message = "Hallo";
        printMessageLength(message);
        message = null;
        printMessageLength(message);
    }

    private static void printMessageLength(String message) {
        System.out.println("Length: " + message.length());
    }
}
   ```

**Stappenplan:**

1. Zet een breakpoint op regel `7` (`System.out.println(...)`).
2. Start de debugger en inspecteer de variabelen.
3. Corrigeer de `NullPointerException`.

**Oplossing:**
   <details>
   <summary>klik hier voor de uitwerking</summary>

   ```java
   private static void printMessageLength(String message){
        if(message==null){
        System.out.println("Message is null.");
        }else{
        System.out.println("Length: "+message.length());
        }
        }
   ```

   </details>

**Oefening 2: ArrayIndexOutOfBoundsException**

**Doel:** Vind de oorzaak van de fout en los deze op.

**Code Voorbeeld:**

```java
   public class ArrayExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        printNumberAtIndex(numbers, 10);
    }

    private static void printNumberAtIndex(int[] array, int index) {
        System.out.println("Number: " + array[index]);
    }
}
   ```

**Stappenplan:**

- Zet een breakpoint op regel `8` (`System.out.println(...)`).
- Start de debugger en inspecteer de variabelen.
- Corrigeer de `ArrayIndexOutOfBoundsException`.

**Oplossing:**
   <details>
   <summary>klik hier voor de uitwerking</summary>

   ```java
   private static void printNumberAtIndex(int[]array,int index){
        if(index< 0||index>=array.length){
        System.out.println("Invalid index: "+index);
        }else{
        System.out.println("Number: "+array[index]);
        }
        }
   ```

   </details>

4. **Oefening 3: ConcurrentModificationException**

**Doel:** Gebruik de debugger om de fout te lokaliseren en op te lossen.

Een `ConcurrentModificationException` kan voorkomen in Java wanneer een verzameling (zoals een List, Set, of Map) wordt
gewijzigd terwijl deze wordt doorlopen met een iterator. Deze uitzondering wordt meestal gegooid om te voorkomen dat er
onvoorspelbaar gedrag optreedt als gevolg van wijzigingen aan de verzameling tijdens iteratie.

**Code Voorbeeld:**

```java
   import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class ConcurrentModificationExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        for (String name : names) {
            if (name.equals("Alice")) {
                names.remove(name);
            }
        }

        System.out.println(names);
    }
}
   ```

**Stappenplan:**

Zet een breakpoint op regel `14` (`names.remove(...)`).
Start de debugger en inspecteer de variabelen.
Corrigeer de `ConcurrentModificationException`.

**Oplossing:**
   <details>
   <summary>klik hier voor de uitwerking</summary>

   ```java
   Iterator<String> iterator=names.iterator();
        while(iterator.hasNext()){
        String name=iterator.next();
        if(name.equals("Bob")){
        iterator.remove();
        }
        }
   ```

   </details>

**Eindopdracht: Complexere Bug Vinden**

**Doel:** Pas de geleerde debugging vaardigheden toe om een complexere fout op te lossen.

**Code Voorbeeld:**

   ```java
   import java.util.HashMap;

import java.util.Map;

public class InventorySystem {
    private Map<String, Integer> inventory = new HashMap<>();

    public static void main(String[] args) {
        InventorySystem system = new InventorySystem();
        system.addItem("Apple", 10);
        system.addItem("Banana", 5);
        system.removeItem("Apple", 5);
        system.removeItem("Banana", 10);
    }

    public void addItem(String item, int quantity) {
        inventory.put(item, inventory.getOrDefault(item, 0) + quantity);
        System.out.println("Added " + quantity + " " + item + "(s)");
    }

    public void removeItem(String item, int quantity) {
        if (inventory.containsKey(item) && inventory.get(item) >= quantity) {
            inventory.put(item, inventory.get(item) - quantity);
            System.out.println("Removed " + quantity + " " + item + "(s)");
        } else {
            System.out.println("Error: Not enough " + item + " in inventory");
        }
    }

}

   ```

**Stappenplan:**

- Zet breakpoints bij `addItem` en `removeItem`.
- Start de debugger en inspecteer de inventaris.
- Corrigeer de `Error` bij het verwijderen van items.

**Hint:** Pas de logica aan zodat `removeItem` geen negatieve waarden veroorzaakt.

**Oplossing**
   <details>
   <summary>klik hier voor de uitwerking</summary>

```java
   public void removeItem(String item,int quantity){
        if(inventory.containsKey(item)){
          int currentQuantity=inventory.get(item);
          if(currentQuantity>=quantity){
            inventory.put(item,currentQuantity-quantity);
            System.out.println("Removed "+quantity+" "+item+"(s)");
          }else{
            System.out.println("Error: Not enough "+item+" in inventory");
          }
          }else{
            System.out.println("Error: Item not found");
          }
        }
```

</details>

**Fun challenge - Kraak de kluis**

- wie kan als eerste het geheime woord vinden?

Pas de toegangscodes aan om toegang te krijgen tot het geheime woord. Gebruik je kennis van debuggen om de codes te vinden

````java

class DebugSafe {
    
public static void main(String[] args) {
String code1 = "";
String code2 = "";
int code3 = 0;

        if (checkCode1(code1) && checkCode2(code2) && checkCode3(code3)) {
            revealSecretWord(code1, code2, code3);
        } else {
            System.out.println("Niet alle codes zijn correct. Probeer het opnieuw.");
        }
    }

    public static boolean checkCode1(String code1) {
        if (code1.length() != 5) {
            return false;
        }
        for (int i = 0; i < code1.length(); i++) {
            char c = code1.charAt(i);
            if (c != 'A' + i) {
                return false;
            }
        }
        return true;
    }

    public static boolean checkCode2(String code2) {
        if (code2.length() != 5) {
            return false;
        }
        for (int i = 0; i < code2.length(); i++) {
            char c = code2.charAt(i);
            if (((Character.isLowerCase(c) && i % 2 == 0) && c != 'z' - i) || ((Character.isUpperCase(c) && i % 2 != 0) && c != 'A' + i)) {
                return false;
            }
        }
        return true;
    }

    public static boolean checkCode3(int code3) {
        int[] numbers = {1000171, 1000172, 1000173, 1000174};
        for (int number : numbers) {
            if (number == code3) {
                return true;
            }
        }
        return false;
    }

    public static void revealSecretWord(String code1, String code2, int code3) {
        int shift1 = code1.charAt(0) - 'A';
        int shift2 = code2.charAt(4) - 'V';
        int shift3 = code3 % 10;
        int totalShift = (shift1 + shift2 + shift3) % 26;

        String encryptedWord = "Ovlyh ola pz jvkpun dlkulzkhf!";
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
