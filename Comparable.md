##A Comparable interfész implementálása

### Deklaráció
```
public interface Comparable<T>{
    int compareTo(T item);
}
```
###Áttekintés
A Comparable interfész a javaban egy adott T típuson teljes rendezést valósít meg. A különféle beépített típusok, mint a listák ( és tömbök) "gyárilag tartalmazzák", lehetővé téve többek közt az alábbi műveleteket:

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
