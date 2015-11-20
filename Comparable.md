##A Comparable interfész implementálása

### Deklaráció
```
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
*  **Object** (`Object`) esetében használjuk a `compareTo` függvényt. Megjegyzendő, hogy a valószínűleg null mezők problémát jelenthetnek, ugyanis ameddig az `x.eqals(null)` mindig hamisat ad vissza, addig a `x.compareTo(null)` `NullPointerException`-t dob
*  **Típusbiztos felsorolások**: Lásd Object
*  **Kollekciók vagy tömbök**:  Az ilyen jellegű adatszerkezeteknél nem indokolt a `compareTo` implementálása. Példának okáért a `List`,`Set`, vagy `Map` adatszerkezetek se valósítját meg a `Comparable` interfészt. Ugyanis a legtöbb kollekcióban nincs határozott sorrendje az elemek bejárásának, így egy elemenkénti összehasonlításnak sincs semmi értelme.
*  A primitív típusok csomagoló osztályai (a `Boolean` kivételével) mind megvalósítják a `Comparable` interfészt

>A `Comparable` interfész helyett használahatunk [Comparator](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html "Comparator objektum") objektumokat alternatívaként. Arra azonban ilyenkor oda kell figyelni, hogy ha a `Comparator` objektum a lehetséges mezők közül csak egy alapján hasonlít össze, az eredmény nem feltétlenül lesz szinkronban az `equals` eredményével!
