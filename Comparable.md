##A Comparable interfész implementálása

### Deklaráció
```
public interface Comparable<T>{
    int compareTo(T item);
}
```
###Felhasználása
A Comparable interfész a jvaban egy adott T típuson teljes rendezést valósít meg. A különféle beépített típusok, mint a listák ( és tömbök) "gyárilag tartalmazza", lehetővé téve többek közt az alábbi műveleteket:
  *[Collections.sort](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#sort(java.util.List) "rendezés") és [Collections.binarySearch](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html#binarySearch(java.util.List,%20T) "bináris keresés") használata listákon
