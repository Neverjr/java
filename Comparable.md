#A Comparable interfész

### Szintaxis
```java
public interface Comparable<T>{
    int compareTo(T item);
}
```
###Áttekintés
A Comparable interfész a javaban egy adott T típuson teljes rendezést valósít meg. Amennyiben egy objektumon megvalósítjuk a `Comparable` interfészt, az alábbi lehetőségek válnak elérhetővé:

*  [Collections.sort](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#sort(java.util.List) "rendezés") és [Collections.binarySearch](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#binarySearch(java.util.List,%20T) "bináris keresés") használata listákon
*  [Arrays.sort](http://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html#sort(byte[]) "rendezés") és [Arrays.binarySearch](http://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html#binarySearch(byte[],%20byte) "bináris keresés") használata tömbökön
*  T típusú objektumok kulcsként való használata [Treeset](http://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html "treeset") és [Treemap](http://docs.oracle.com/javase/7/docs/api/java/util/TreeMap.html "treemap") adatszerkezetekben

###Követelmények
A jól implementált Comparable interfész az alábbi tulajdonságokkal kell rendelkezzen:
*  **Antikommutativitás**, azaz egy `x.compareTo(y)` pontosan ellentéte a`y.compareTo(x)` műveletnek.
*  **Kivétel szimmetria**, azaz egy `x.compareTo(y)` pontosan ugyanazokat a kivételeket kell kiváltsa, mint egy `y.compareTo(x)`.
  * Például ha `x = new X()` és `y = null`, akkor mind az `x.compareTo(y)`, mind az `y.compareTo(x)` `NullPointerException`-t vált ki.
*  **Tranzitivitás**, azaz ha `x.compareTo(y) > 0` és `y.compareTo(z) > 0`, akkor `x.compareTo(z) > 0` is igaz kell legyen
*  **Konzisztencia az `equals` függénnyel**: *Nem kötelező, de erősen ajánlott!* Azaz `x.compareTo(y)` akkor és csak akkor 0, ha`x.equals(y)`
  * Annak érdekében, hogy a rendezett kollekciók (mint például a `Treeset`) is helyesen működjenek, ezekben az esetekben a konzisztencia megőrzése kötelező az `equals` függvénnyel

###Megvalósítás
> A `compareTo` hatékonyságát nagyban javíthatja az objektum adattagjainak sorrendje, azaz lehetőség szerint kezdjünk mindig a lehető legeltérőbb elemmel.

Az általános típusokon a rendezés az alábbi módszerekkel valósítható meg:
*  **számszerű primitívek** (`int`, `short`, `byte`,`long`, illetve ide tartozik a `char`): < vagy > operátorral. A lebegőpontos számoknál(`float`, `double`) a kerekítések miatt ezek nem használhatóak. Helyettük használjuk a [Float.compare(float, float)](http://docs.oracle.com/javase/7/docs/api/java/lang/Float.html#compare(float,%20float) "Float összehasonlítás"), illetve a [Double.compare(double, double)](http://docs.oracle.com/javase/7/docs/api/java/lang/Double.html#compare(double,%20double) "Double összehasonlítás") függvényeket.
*  **logikai** (`boolean`) típusnál használjuk a `(x && !y)` formulát
*  **Object** (`Object`) esetében használjuk a `compareTo` függvényt. Megjegyzendő, hogy a valószínűleg null mezők problémát jelenthetnek, ugyanis ameddig az `x.equals(null)` mindig hamisat ad vissza, addig a `x.compareTo(null)` `NullPointerException`-t dob
*  **Típusbiztos felsorolások**: Lásd Object
*  **Kollekciók vagy tömbök**:  Az ilyen jellegű adatszerkezeteknél nem indokolt a `compareTo` implementálása. Példának okáért a `List`,`Set`, vagy `Map` adatszerkezetek se valósítját meg a `Comparable` interfészt. Ugyanis a legtöbb kollekcióban nincs határozott sorrendje az elemek bejárásának, így egy elemenkénti összehasonlításnak sincs semmi értelme.
*  A primitív típusok csomagoló osztályai (1.5-ösnél korábbi verziókban a `Boolean` kivételével) mind megvalósítják a `Comparable` interfészt

>A `Comparable` interfész helyett átadhatunk [Comparator](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html "Comparator objektum") objektumokat paraméterként. Arra azonban ilyenkor oda kell figyelni, hogy ha a `Comparator` objektum a lehetséges mezők közül csak egy alapján hasonlít össze, az eredmény nem feltétlenül lesz szinkronban az `equals` eredményével!

###Implementáció
Az alábbiakban egy `Comparable` implementáció látható, amely 1.5-ösnél újabb java verziókban fordul:

```java
import java.util.*;
import java.io.*;

public final class Account implements Comparable<Account> {
  
  enum AccountType {CASH, MARGIN, RRSP};

   public Account (
      String aFirstName,
      String aLastName,
      int aAccountNumber,
      int aBalance,
      boolean aIsNewAccount,
      AccountType aAccountType
  ) {
      //..parameter validations elided
      fFirstName = aFirstName;
      fLastName = aLastName;
      fAccountNumber = aAccountNumber;
      fBalance = aBalance;
      fIsNewAccount = aIsNewAccount;
      fAccountType = aAccountType;
   }

  /**
  * @param aThat is a non-null Account.
  *
  * @throws NullPointerException if aThat is null.
  */
  @Override public int compareTo(Account aThat) {
    final int BEFORE = -1;
    final int EQUAL = 0;
    final int AFTER = 1;

    //this optimization is usually worthwhile, and can
    //always be added
    if (this == aThat) return EQUAL;

    //primitive numbers follow this form
    if (this.fAccountNumber < aThat.fAccountNumber) return BEFORE;
    if (this.fAccountNumber > aThat.fAccountNumber) return AFTER;

    //booleans follow this form
    if (!this.fIsNewAccount && aThat.fIsNewAccount) return BEFORE;
    if (this.fIsNewAccount && !aThat.fIsNewAccount) return AFTER;

    //objects, including type-safe enums, follow this form
    //note that null objects will throw an exception here
    int comparison = this.fAccountType.compareTo(aThat.fAccountType);
    if (comparison != EQUAL) return comparison;

    comparison = this.fLastName.compareTo(aThat.fLastName);
    if (comparison != EQUAL) return comparison;

    comparison = this.fFirstName.compareTo(aThat.fFirstName);
    if (comparison != EQUAL) return comparison;

    if (this.fBalance < aThat.fBalance) return BEFORE;
    if (this.fBalance > aThat.fBalance) return AFTER;

    //all comparisons have yielded equality
    //verify that compareTo is consistent with equals (optional)
    assert this.equals(aThat) : "compareTo inconsistent with equals.";

    return EQUAL;
  }

   /**
   * Define equality of state.
   */
   @Override public boolean equals(Object aThat) {
     if (this == aThat) return true;
     if (!(aThat instanceof Account)) return false;

     Account that = (Account)aThat;
     return
       ( this.fAccountNumber == that.fAccountNumber ) &&
       ( this.fAccountType == that.fAccountType ) &&
       ( this.fBalance == that.fBalance ) &&
       ( this.fIsNewAccount == that.fIsNewAccount ) &&
       ( this.fFirstName.equals(that.fFirstName) ) &&
       ( this.fLastName.equals(that.fLastName) )
     ;
   }

   /**
   * A class that overrides equals must also override hashCode.
   */
   @Override public int hashCode() {
     int result = HashCodeUtil.SEED;
     result = HashCodeUtil.hash( result, fAccountNumber );
     result = HashCodeUtil.hash( result, fAccountType );
     result = HashCodeUtil.hash( result, fBalance );
     result = HashCodeUtil.hash( result, fIsNewAccount );
     result = HashCodeUtil.hash( result, fFirstName );
     result = HashCodeUtil.hash( result, fLastName );
     return result;
   }

   //PRIVATE

   private String fFirstName; //non-null
   private String fLastName;  //non-null
   private int fAccountNumber;
   private int fBalance;
   private boolean fIsNewAccount;

   /**
   * Type of the account, expressed as a type-safe enumeration (non-null).
   */
   private AccountType fAccountType;

   /**
   * Exercise compareTo.
   */
   public static void main (String[] aArguments) {
     //Note the difference in behaviour in equals and compareTo, for nulls:
     String text = "blah";
     Integer number = new Integer(10);
     //x.equals(null) always returns false:
     System.out.println("false: " + text.equals(null));
     System.out.println("false: " + number.equals(null) );
     //x.compareTo(null) always throws NullPointerException:
     //System.out.println( text.compareTo(null) );
     //System.out.println( number.compareTo(null) );

     Account flaubert = new Account(
      "Gustave", "Flaubert", 1003, 0,true, AccountType.MARGIN
     );

     //all of these other versions of "flaubert" differ from the
     //original in only one field
     Account flaubert2 = new Account(
       "Guy", "Flaubert", 1003, 0, true, AccountType.MARGIN
     );
     Account flaubert3 = new Account(
       "Gustave", "de Maupassant", 1003, 0, true, AccountType.MARGIN
     );
     Account flaubert4 = new Account(
       "Gustave", "Flaubert", 2004, 0, true, AccountType.MARGIN
     );
     Account flaubert5 = new Account(
       "Gustave", "Flaubert", 1003, 1, true, AccountType.MARGIN
     );
     Account flaubert6 = new Account(
       "Gustave", "Flaubert", 1003, 0, false, AccountType.MARGIN
     );
     Account flaubert7 = new Account(
       "Gustave", "Flaubert", 1003, 0, true, AccountType.CASH
     );

     System.out.println( "0: " +  flaubert.compareTo(flaubert) );
     System.out.println( "first name +: " +  flaubert2.compareTo(flaubert) );
     //Note capital letters precede small letters
     System.out.println( "last name +: " +  flaubert3.compareTo(flaubert) );
     System.out.println( "acct number +: " +  flaubert4.compareTo(flaubert) );
     System.out.println( "balance +: " +  flaubert5.compareTo(flaubert) );
     System.out.println( "is new -: " +  flaubert6.compareTo(flaubert) );
     System.out.println( "account type -: " +  flaubert7.compareTo(flaubert) );
   }
}
```
>[Forrás](http://www.javapractices.com/topic/TopicAction.do?Id=10 "Forrás")
