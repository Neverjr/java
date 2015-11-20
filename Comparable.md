##A Comparable interfész implementálása

### Deklaráció
```
public interface Comparable<T>{
    int compareTo(T item);
}
```
###Felhasználása
A Comparable interfész a javaban egy adott T típuson teljes rendezést valósít meg. A különféle beépített típusok, mint a listák ( és tömbök) "gyárilag tartalmazza", lehetővé téve többek közt az alábbi műveleteket:

*  [Collections.sort](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#sort(java.util.List) "rendezés") és [Collections.binarySearch](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#binarySearch(java.util.List,%20T) "bináris keresés") használata listákon
*  [Arrays.sort](http://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html#sort(byte[]) "rendezés") és [Arrays.binarySearch](http://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html#binarySearch(byte[],%20byte) "bináris keresés") használata tömbökön
*  T típusú objektumok kulcsként való használata [Treeset](http://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html "treeset") és [Treemap](http://docs.oracle.com/javase/7/docs/api/java/util/TreeMap.html "treemap") adatszerkezetekben
