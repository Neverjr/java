#A boxing helyes használata

##Áttekintés
A boxing ("dobozolás") művelete az 1.5-ös java újtása volt, hogy megkönnyítse a konverziót a primitívek (`int`, `boolean`, `char`, ...) és a csomagoló osztályaik (`Integer`, `Boolean`, 
`Character`,...) között. 
A dobozolás használatával a kód olvashatóbbá és tömörebbé válik.

##Tulajdoságok

A boxingnak két biztosított szempotja van:
*  *Auto-boxing*: Ami automatikus konverzióra utal például az `int` és az `Integer` között
  * Például: `int number = new Integer(4)`, ahol number értéke 4 lesz
*  *Auto-unboxing*: Automatikus konverzió például `Boolean` és `boolean` között
  * Például: `Boolean bool = true`, ahol bool értéke igaz lesz
  
A boxing részben elrejti a primitívek és az objektumok közti különbséget, de nem szünteti meg. Többek között az alábbiak tulajdonságok se változak:
*  Az objektumok lehetek `null` értékűek, míg a primitívek nem
*  Az objetumoknak van identitása és állapota, míg a primitíveknek csak állapota (értéke)

>Bizonyos esetekben ezek problémákat okozhatnak a dobozolás használatakor.

Emlékeztetőül:
  * Legyünk óvatosak a `null` értékekkel. Egy `null` elem automatikus kidobozolása `NullPointerexception`-t okoz
  * Mindig megfelelő körültekintéssel hasonltsunk össze két elemet a `==` operátorral, vagy az `equals` függvénnyel

##Az összehasonltás szabályai

Ha x és y is primitív vagy csomagoló objektum:

|**Művelet**  |Két primitív             |Két objektum                 |
|-------------|:-----------------------:|----------------------------:|
|`x == y`     |értékek összehasonlítása | referenciák összehasonlítása|
|`x.equals(y)`|fordítási hiba           |értékek összehasonlítása     |

Abban az esetben ha az egyik érték primitít, a másik meg a megfelelő csomagoló objektum:

|**Művelet**  |**Viselkedés**                                                                                     |
|-------------|:-------------------------------------------------------------------------------------------------:|
|`x == y`     |primitívekként veszi figyelembe és összehasonlítja az értéket                                      |
|`x.equals(y)`|nem fordul, ha x primitív; ellenkező esetben objektumnak tekinti őket és értéket hasonlít össze    |


##Példa

```java
import java.util.*;

public final class BoxingExamples {

  public static final void main(String... aArgs){
    //pass Integer where int expected
    explode(new Integer(3));

    //pass literal where Boolean expected
    tellTruth(true);

    //calculate "int-erchangably" with int and Integer
    Integer integerYear = new Integer(1989);
    Integer otherIntegerYear = integerYear + 10;
    int intYear = integerYear + new Integer(15);
    log(integerYear.toString());
    log(otherIntegerYear.toString());
    System.out.println(intYear);

    /*
    * Comparison of primitives and wrapper objects using == and equals.
    *
    * When both items are of the same type :
    *             2 primitives          2 objects
    * ----------------------------------------------------------
    * ==       :  value                 identity
    * equals() :  not applicable        value
    *
    *
    * When one item is a primitive, and the other is an object :
    * ==          :  treat as two primitives
    * x.equals(y) :  treat as two objects; do not compile if x is primitive
    */
    intYear = 1880;
    integerYear = new Integer(1880);
    if (intYear == integerYear){
      log("intYear == integerYear: TRUE"); // yes
    }
    else {
      log("intYear == integerYear : FALSE");
    }
    if (integerYear.equals(intYear)){
      log("integerYear.equals(intYear): TRUE"); //yes
    }
    else {
      log("integerYear.equals(intYear): FALSE");
    }
    //does not compile "int cannot be dereferenced" :
    //intYear.equals(integerYear);

    intYear = 1881; //new value
    if (intYear == integerYear){
      log("intYear == integerYear: TRUE");
    }
    else {
      log("intYear == integerYear : FALSE"); // yes
    }
    if (integerYear.equals(intYear)){
      log("integerYear.equals(intYear): TRUE");
    }
    else {
      log("integerYear.equals(intYear): FALSE"); //yes
    }
  }

  // PRIVATE
  private static void explode(int aNumTimes){
    log("Exploding " + aNumTimes + " times.");
  }

  private static void tellTruth(Boolean aChoice){
    //instead of if ( aChoice.booleanValue() ) {
    if (aChoice) {
      log("Telling truth.");
    }
    else {
      log("Lying like a rug.");
    }
  }

  private static void log(String aText){
    System.out.println(aText);
  }
} 
```

>[Forrás](http://javapractices.com/topic/TopicAction.do?Id=197 "Forrás")
