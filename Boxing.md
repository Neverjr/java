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

>[Forrás](http://javapractices.com/topic/TopicAction.do?Id=197 "Forrás")
