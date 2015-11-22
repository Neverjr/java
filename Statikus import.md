#Statikus importok használata

##Áttekintés

A statikus importok lehetővé teszik, hogy egy osztály minőstés nélkül hivatkozzon egy másikra. Ész nélüli használata azonban sokkal átláthatatlanabá és nehezebben érthetővé teszik a kódot.

##Használata

Bizonyos esetekben azonban "bocsánatos bűn" a statikus import haszálata. Ilyen helyzet, amikor konstans osztályokat importálunk.
Például matematikai programokban gyakran fordul elő a `Math.PI`, ami ajavaban a `java.lang.Math` statikus osztályban szereplő konstas. Ilyenhelyzetekben az `import java.lang.Math.*` lehetővé teszi, hogy minőstett név nélkül hivatkozzunk a pi-re.
  * Pi használata statikus importtal: `double pi = PI`
  * Pi haszálata statikus import nélkül: `double pi2 = Math.PI`
