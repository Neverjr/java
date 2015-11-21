#Az Override annotáció

###Szintaxis
```java
@Override
public void method(){//...}
```
###Leírás
Az `@Override` annotáció az 1.5-ös Verzióval került be a java nyelvbe, többé-kevésbé mint egy metódus módosító eszköz. Ha egy függvényt vagy metódust ezzel az annotációval jelölünk, 
akkor jelezzük a fordítónak, hogy az adott alprogram mindenképpen felülírja egy őstípus adott eljárását, legyen az egy interfészben vay egy absztrakt ősosztályba.
>Amikor az `@Override`-ot bevezették az 1.5-ös javaban, csak és kizárólag ősosztályokból örökölt metódusok felüldefiniálását jelülhettük vele, interfészekből impelentáltakat nem.
Ezt a lehetőséget a 7-es java (1.7) hozta el.