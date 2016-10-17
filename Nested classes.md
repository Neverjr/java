#Beágyazott osztályok

##Áttekintés

A java nyelv lehetőséget biztosít arra, hogy osztályokat deklaráljunk másik osztályok belsejébe, ami egy rendkívül hasznos eszköz, ugyanakkor körültekintően kell használni. Ennek a módszernek több változata is ismert, ezekről a lentiekben bővebben is beszélünk.

##Variációk

|                 | Statikus                    | Nem statikus                     | Névtelen               |
| --------------- | :-------------------------: |  :-----------------------------: | :--------------------: |
| **Nem lokális** | Statikus beágyazott osztály | Belső osztály                    | *(Nem lehetséges)*     |
| **Lokális**     | *(Nem lehetséges)*          | Lokális belső osztály            | Névtelen belső osztály |

###Statikus beágyazott osztály

Egy java osztály (vagy interfész) tartalmazhat egy másik osztályt (vagy interfészt), mint statikus adattagot ( interfészek esetében a belső osztályt nem kötelező expliciten megjelölni a *static* kulcsszóval, mivel minden adattag impliciten *public* és *static* módosítót kap.

####Összefoglaló
  * Egy statikus beágyazott osztály láthatóságát (*public*, *protected*,*stb.*) a tartalmazó osztály határozza meg.
  * Egy statikkus beágyazott osztály **KülsőOsztályNév.StatikusBeágyazottOsztályNév** szintaxissal érhető el.
  * Ha interfészben deklarálunk statikus beágyazott osztályt, az impliciten *public* és *static* lesz. Ennek oka, hogy egy interfészben minden adattag *public* és *static*. Ez beágyazott osztályok esetében sincs másképp.
  * A statikus beágyazott osztályok lehetnek *abstract* vagy *final* osztályok (de a kettő együtt természetesen soha).
  * A statikus beágyazott osztályok kiterjeszthetnek más osztályokat ( akár a saját tartalmazó osztályukat is).
  * A statikus beágyazott osztályok tartalmazhatnak statikus adattagokat (ellentétben a többi belső osztállyal, ezt lásd később).
  * A statikus belső osztályok hozzáférnek a tartalmazó osztály statikus (osztályszintű) tagjaihoz (adattagok és tagfüggvények). Példányszintű tagokat értelemszerűen nem érhetnek el.
  * A külső osztály a beágyazott statikus osztály minden tagjához (még a *private* láthatóságúakhoz is) hozzáférnek a belső osztály egy példányán keresztül.
  
###Példa

```java
class CoordTypes{
	
	public static class Point2D{
		int x_coord, y_coord;
		
		public Point2D(){
			this(0,0);
		}
		
		public Point2D(int first, int second){
			x_coord = first;
			y_coord = second;
		}
		
		@Override
		public String toString(){
			return "["+x_coord+";"+y_coord+"]";
		}
		
		//Point2D egyéb tagjai
	}
	
	//CoordTypes egyéb tagjai
}

public class TestClass{
	
	public static void main(String[] arguments){
		//Tekintve, hogy a Point2D statikus beágyzott osztály,
		//a külső osztályon keresztül hozzá tudunk férni a CoordTypes.Point2D szintaxissal.
		//Arra viszont figyeljünk, hogy ehhez nem kell létrehozni a
		//CoordTypes osztály példányát
		
		CoordTypes.Point2D point = new CoordTypes.Point2D(10,7);
		System.out.println("Our coord is the following: "+point);
	}
	
}
```

###Belső osztály

Belső osztályt vagy interfészt deklarálhatunk nem statikus, azaz példányszintű adattagként is. Fontos megjegyezni, hogy ez a fajta osztálytípus csak és kizárólag egy másik osztályban készíthető ( tekintve, hogy minden adattag impliciten *static* egy interfészben).
Ilyen esetekben a tartalmazó és a belső osztály (interfész) kapcsolatát leginkább a családtagokéhoz lehet hasonlítani. Hogy ez alatt mégis mit kell érteni? Azt, hogy mindketten hozzáférnek a másik minden tagjához, beleértve a *private* módosítóval ellátottakat is. 

Ugyanakkor egy lényeges különbség mégis akad.
Ha a belső osztályból szeretnénk hozzáférni a külső valamely tagjához ( legyen az adattag/tagfüggvény, még a *private*-ek is), ezt mindenféle nehézség nélkül megtehetjük. Azonban, ha ezt a másik irányba szeretnénk megtenni, a helyzet már nem ilyen egyszerű. A külső osztály csak a belső egy példányán keresztül férhet hozzá annak tagjaihoz (de ekkor természetesen mindegyikhez). Magyarán először létre kell hozni a belső osztály egy példányát adattagként a külső osztályban. Ennek módja: **InnerClass ic = this.new InnerClass();**

Noha az eddigiek alapján joggal feltételezhetjük, hogy szinte semmi megkötést nem tesz a Java az ilyen kapcsolatokra, egy lényeges dolgot azért szem előtt kell tartanunk: Példányszintű belső osztály nem tartalmazhat statikus deklarációt (ennek végiggondolása az olvasó feladata).

####Összefoglaló
  * A belső osztály láthatóságát (úgy, mint *public*,*private*, stb.) a tartalmazó osztály határozza meg.
  * Hasonlóan a legfelső szinten lévő osztályokhoz, a belső osztályok is kiterjeszthetnek másik osztályokat, vagy implementálhatnak interfészeket (ahogyan egy belső interfész is kibővíthet más interfészeket).
  * Egy belső osztály ellátható *final* **vagy** *abstract* módosítóval.
  * Noha egy belső osztály is tartalmazhat saját belső osztályt (vagy interfészt), azonban a túlbonyolított struktúrák elkerülése végett tanácsos kerülni a túlzott egymásba ágyazást.
  * A belső osztály megkötés nélkül hozzáfér a tartalmazó osztály minden tagjához.
  * Fordítva viszont ez nem igaz, a tartalmazó osztály csak a belső egy példányán keresztül fér hozzá a tagjaihoz. Ennek szintaxisa: **InnerClass ic = this.new InnerClass();**.
  
###Példa
