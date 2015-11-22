#A boxing helyes használata

##Boxing
A boxing ("dobozolás") művelete az 1.5-ös java újtása volt, hogy megkönnyítse a konverziót a primitívek (`int`, `boolean`, `char`, ...) és a csomagoló osztályaik (`Integer`, `Boolean`, 
`Character`,...) között. 
A dobozolás használatával a kód olvashatóbbá és tömörebbé válik.

A boxignak két biztosított szempotja van:
*  *Auto-boxing*: Ami automatikus konverzióra utal például az `int` és az `Integer` között
  *Például: `int number = new Integer(4)`, ahol numbe értéke 4 lesz
*  *Auto-unboxing*: Automatikus konverzió például `Boolean` és `boolean` között

>[Forrás](http://javapractices.com/topic/TopicAction.do?Id=197 "Forrás")