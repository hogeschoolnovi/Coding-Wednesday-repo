## React workshop overzicht 

1. **Inleidende Theorie (10 minuten)**
    - **Wat is Refactoring?**
        - Refactoring is het proces van het wijzigen van de interne structuur van software zonder het externe gedrag te veranderen.
    - **Waarom Refactoren?**
        - Verbeter de leesbaarheid, onderhoudbaarheid en prestaties van code.

   **Bronnen voor verdere verdieping:**
    - [Refactoring in IntelliJ IDEA](https://www.jetbrains.com/help/idea/refactoring-source-code.html)
    - [SOLID Principes](https://en.wikipedia.org/wiki/SOLID)
    - [Clean Code Boek door Robert C. Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

2. **Oefening 1: Method Extracting (40 minuten)**
    - **Code Voorbeeld:**
   ```javascript
   import React from 'react';

   function Invoice({ customerName, amount }) {
       return (
           <div>
               <h1>Invoice</h1>
               <hr />
               <p>Customer: {customerName}</p>
               <p>Amount: {amount}</p>
               <hr />
               <p>Thank you for your business!</p>
           </div>
       );
   }

   export default Invoice;
   ```
    - **Uitdaging:**
        1. Refactor de `Invoice` component door verschillende delen naar afzonderlijke componenten te verplaatsen.
        2. Gebruik *Extract Method* in IntelliJ IDEA.

    - **Oplossing:**
   ```javascript
   import React from 'react';

   function Invoice({ customerName, amount }) {
       return (
           <div>
               <InvoiceHeader />
               <InvoiceDetails customerName={customerName} amount={amount} />
               <InvoiceFooter />
           </div>
       );
   }

   function InvoiceHeader() {
       return (
           <div>
               <h1>Invoice</h1>
               <hr />
           </div>
       );
   }

   function InvoiceDetails({ customerName, amount }) {
       return (
           <div>
               <p>Customer: {customerName}</p>
               <p>Amount: {amount}</p>
               <hr />
           </div>
       );
   }

   function InvoiceFooter() {
       return <p>Thank you for your business!</p>;
   }

   export default Invoice;
   ```

3. **Code Smells (10 minuten)**
    - **Wat zijn Code Smells?**
        - "Indicatoren" van slecht ontworpen code.

   **Bronnen voor verdere verdieping:**
    - [Code Smells](https://refactoring.guru/refactoring/smells)

4. **Oefening 2: Extract Class en Move Method (40 minuten)**
    - **Code Voorbeeld:**
   ```javascript
   class Customer {
       constructor(name, address, phoneNumber, orders) {
           this.name = name;
           this.address = address;
           this.phoneNumber = phoneNumber;
           this.orders = orders;
       }

       getTotalOrderValue() {
           let total = 0;
           for (let order of this.orders) {
               total += order.value;
           }
           return total;
       }

       hasLatePayments() {
           for (let order of this.orders) {
               if (order.isLate) {
                   return true;
               }
           }
           return false;
       }
   }
   ```

    - **Uitdaging:**
        1. Verplaats de logica van `getTotalOrderValue` en `hasLatePayments` naar een nieuwe klasse `OrderHistory`.
        2. Gebruik *Extract Class* en *Move Method* in IntelliJ IDEA.
        3. Refactor de `Customer` klasse om samen te werken met `OrderHistory`.

    - **Oplossing:**
   ```javascript
   class Customer {
       constructor(name, address, phoneNumber, orders) {
           this.name = name;
           this.address = address;
           this.phoneNumber = phoneNumber;
           this.orderHistory = new OrderHistory(orders);
       }

       getTotalOrderValue() {
           return this.orderHistory.getTotalOrderValue();
       }

       hasLatePayments() {
           return this.orderHistory.hasLatePayments();
       }
   }

   class OrderHistory {
       constructor(orders) {
           this.orders = orders;
       }

       getTotalOrderValue() {
           let total = 0;
           for (let order of this.orders) {
               total += order.value;
           }
           return total;
       }

       hasLatePayments() {
           for (let order of this.orders) {
               if (order.isLate) {
                   return true;
               }
           }
           return false;
       }
   }
   ```

5. **Break (10 minuten)**

6. **Oefening 3: Inline Method en Rename Refactoring (30 minuten)**
    - **Code Voorbeeld:**
   ```javascript
   class Product {
       constructor(price) {
           this.price = price;
       }

       getDiscountedPrice() {
           return this.applyDiscount(this.price);
       }

       applyDiscount(originalPrice) {
           return originalPrice * 0.9;
       }
   }
   ```
    - **Uitdaging:**
        1. Gebruik *Inline Method* om `applyDiscount` samen te voegen met `getDiscountedPrice`.
        2. Gebruik *Rename Refactoring* om `price` te hernoemen naar `originalPrice`.

    - **Oplossing:**
   ```javascript
   class Product {
       constructor(originalPrice) {
           this.originalPrice = originalPrice;
       }

       getDiscountedPrice() {
           return this.originalPrice * 0.9;
       }
   }
   ```

7. **Theorie: Refactoring Tools in IntelliJ IDEA (10 minuten)**
    - **Overzicht van Refactoring Tools:**
        - *Extract Method / Class / Interface*
        - *Inline Method / Variable*
        - *Rename*
        - *Move Method / Class*
        - *Change Signature*

   **Bronnen voor verdere verdieping:**
    - [Refactoring Tools in IntelliJ IDEA](https://www.jetbrains.com/help/idea/refactoring-source-code.html)

8. **Eindopdracht (40 minuten): Verbeter een Project met Refactoring Tools**
    - **Doel:** Verbeter een bestaande codebase met behulp van refactoring tools in IntelliJ IDEA.
    - **Code Voorbeeld:**
   ```javascript
   class Library {
       constructor(books) {
           this.books = books;
       }

       getBooksByAuthor(author) {
           let result = [];
           for (let book of this.books) {
               if (book.author === author) {
                   result.push(book);
               }
           }
           return result;
       }

       getBooksPublishedAfter(year) {
           let result = [];
           for (let book of this.books) {
               if (book.publicationYear > year) {
                   result.push(book);
               }
           }
           return result;
       }
   }

   class Book {
       constructor(title, author, publicationYear) {
           this.title = title;
           this.author = author;
           this.publicationYear = publicationYear;
       }
   }
   ```
    - **Uitdaging:**
        1. Maak een nieuwe klasse `BookFilter` die filtermethoden bevat.
        2. Verplaats de filtermethoden naar `BookFilter`.
        3. Pas de `Library` klasse aan om `BookFilter` te gebruiken.

    - **Oplossing:**
   ```javascript
   class Library {
       constructor(books) {
           this.books = books;
           this.bookFilter = new BookFilter();
       }

       getBooksByAuthor(author) {
           return this.bookFilter.getBooksByAuthor(this.books, author);
       }

       getBooksPublishedAfter(year) {
           return this.bookFilter.getBooksPublishedAfter(this.books, year);
       }
   }

   class BookFilter {
       getBooksByAuthor(books, author) {
           let result = [];
           for (let book of books) {
               if (book.author === author) {
                   result.push(book);
               }
           }
           return result;
       }

       getBooksPublishedAfter(books, year) {
           let result = [];
           for (let book of books) {
               if (book.publicationYear > year) {
                   result.push(book);
               }
           }
           return result;
       }
   }

   class Book {
       constructor(title, author, publicationYear) {
           this.title = title;
           this.author = author;
           this.publicationYear = publicationYear;
       }
   }
   ```

### Nuttige links en documentatie
- [Refactoring in IntelliJ IDEA](https://www.jetbrains.com/help/idea/refactoring-source-code.html)
- [SOLID Principes](https://en.wikipedia.org/wiki/SOLID)
- [Clean Code Boek door Robert C. Martin](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
- [Code Smells](https://refactoring.guru/refactoring/smells)

Veel succes met het implementeren en verbeteren van je code!