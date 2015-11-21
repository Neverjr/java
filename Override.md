#Az Override annotáció

###Szintaxis
```java
@Override
public void method(){...}
```
###Leírás
Az `@Override` annotáció az 1.5-ös verzióval került be a java nyelvbe, többé-kevésbé mint egy metódus módosító eszköz. Ha egy függvényt vagy metódust ezzel az annotációval jelölünk, 
akkor jelezzük a fordítónak, hogy az adott alprogram mindenképpen felülírja egy őstípus adott eljárását, legyen az egy interfészben vay egy absztrakt ősosztályban.
>Amikor az `@Override`-ot bevezették az 1.5-ös javaban, csak és kizárólag ősosztályokból örökölt metódusok felüldefiniálását jelülhettük vele, interfészekből impelentáltakat nem.
Ezt a lehetőséget a 7-es java (1.7) hozta el.

###Használata
Az `@Override` annotáció legáltalánosabb felhasználási területe az `Object` műveleteinek felüldefiniálása.

```java
@Override public String toString(){...}
@Override public boolean equals(Object){...}
@Override public int hashCode(){...}
```

A legprózaibb ok azonban, amiért az `@Override` annotációt kitalálták, az az, hogy védjen a kevésbé látványos, ugyanakkor annál bosszantóbb elírásoktól.
Példának okáért a 
```java 
@Override public int hashcode(){...} 
``` 
egyáltalán nem egy felüldefiniálás, mert nem egyezik meg a neve  a
```java
@Override public int hashCode(){...}
```
nevével, mivel csupa kisbetűvel írtuk. Akárhogy is, ez fordulna, viszont használat közben kellemetlen meglepetések érnének. Ugyanez érvényes akkor is ha a paraméterlista tér el.
Ekkor ugyanis túlterhelésről beszélünk, ami szintén nehezen detektálható hibákhoz vezet a későbbiekben.
Az `@Override` használatával viszont ezekelkerülhetőek.

###Konklúzió
Érdemes tehát minél hamarabb felvenni a jó szokások közé, hogy metódus felüldefiniálásánál tegyük elé az `@Override` annotációt.
>És ne hallgassunk az olyan önjelölt 'programozókra', akik szerint az `@Override` csak egy fícsör a nyelvben...

>[Forrás](http://www.javapractices.com/topic/TopicAction.do?Id=223 "Forrás")
