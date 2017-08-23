# Statikus importok használata

## Áttekintés

A statikus importok lehetővé teszik, hogy egy osztály minőstés nélkül hivatkozzon egy másikra. Ész nélüli használata azonban sokkal átláthatatlanabá és nehezebben érthetővé teszik a kódot.

## Használata

Bizonyos esetekben azonban "kifejezetten hasznos a statikus import. Ilyen helyzet, amikor konstans osztályokat importálunk.
Például matematikai programokban gyakran fordul elő a `Math.PI`, ami javaban a `java.lang.Math` konstans osztályban szereplő konstas. Ilyenhelyzetekben az `import java.lang.Math.*` lehetővé teszi, hogy minőstett név nélkül hivatkozzunk a pi-re.
  * Pi használata statikus importtal: `double pi = PI`
  * Pi haszálata statikus import nélkül: `double pi2 = Math.PI`

## Példa

```java
import java.util.*;
import static java.util.Collections.*;

public final class StaticImporter {

  public static void main(String... aArgs){
    List<String> things = new ArrayList<>();
    things.add("blah");

    //This looks like a simple call of a method belonging to this class:
    List<String> syncThings = synchronizedList(things);

    //However, it actually resolves to :
    //List<String> syncThings = Collections.synchronizedList(things);
  }
} 
```
 
