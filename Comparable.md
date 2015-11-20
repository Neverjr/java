##A Comparable interfész implementálása

### Deklaráció
```
public interface Comparable<T>{
    int compareTo(T item);
}
```
###Felhasználása
A Comparable interfész a jvaban egy adott T típuson teljes rendezést valósít meg. A különféle beépített típusok, mint a listák ( és tömbök) "gyárilag tartalmazza", lehetővé téve többek közt az alábbi műveleteket:
  *This is [an example](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#sort(java.util.List) "Title") inline link. é Collections.binarySearch használata listákon
