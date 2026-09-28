# 1 Technologie stylusu

Některá zařízení umožňují psát rukou pomocí digitální tužky, neboli stylusu. Mezi tato zařízení spadají například tablety, některé telefony, kreslící podložky k počítači nebo chytré zápisníky.
Ačkoli existuje více technologií snímání stylusu, v dnešní době téměř všechna psací zařízení využívají buďto stylus aktivní nebo pasivní.

## 1.1 Aktivní stylus

Technologie využívající aktivní stylus spočívají v implementaci elektrických obvodů včetně baterie přímo do těla stylusu. Tužka tedy sama generuje signál, který následně zařízení snímá a určuje polohu stylusu.
Aktivní stylus se používá především v kombinaci s technologií kapacitivního snímání dotyku, kde tužka simuluje lidský dotyk aplikováním slabého elektrického signálu.

Hlavní výhoda tohoto typu chytré tužky spočívá v tom, že obsahuje vlastní baterii, a tím pádem může se zařízením komunikovat např. přes Bluetooth nebo Wi-Fi. Také je možno implementovat různé senzory přímo do těla stylusu, které mohou sloužit k detekci přítlaku, náklonu tužky nebo třeba stisku tlačítek.

## 1.2 Pasivní stylus

Narozdíl od aktivních stylusů v sobě tužka neobsahuje žádnou baterii. Namísto toho zařízení kompatibilní s pasivním stylusem obsahuje speciální vrstvu zvanou digitizér, která vysílá elektromagnetické vlny, jež jsou následně odráženy[^1] stylusem zpět a detekovány opět zařízením.

Velkou výhodou je preciznost. Díky přesnému měření elektromagnetického pole je možno zachytit polohu stylusu na desetiny milimetru přesně, což umožňuje detailní práci. Zároveň může být stylus velmi lehký, jelikož neobsahuje těžkou baterii a má v sobě minimum součástek. Nemusí se tedy dobíjet.

Na druhou stranu, absence baterie může být i nevýhodou, neboť stylus funguje pouze v blízkosti zařízení, což znemožňuje použití pokročilejších funkcí, jako například komunikaci přes Bluetooth.

[^1]: Ve skutečnosti jde o rezonanci v obvodu stylusu, která má za následek zpětnou indukci magnetického pole (viz kapitola 3).

# 2 EMR digitizér

Nyní už se dostáváme ke klíčové součásti zařízení, bez níž by snímání tužky nefungovalo - k EMR[^2] digitizéru. Tato část obvodu se stará o dvě důležité věci - vysílání a detekci elektromagnetických vln. Tyto dvě části mohou být oddělené - mohou mít zvlášť obvod na vysílání a zvlášť na přijímání. Většina zařízení však volí rozličnou strategii - mít pouze jeden obvod s jednou sadou antén a mezi dvěma režimy přepínat.

## 2.1 Vysílání

Aby zařízení mohlo vysílat elektromagnetické vlny, potřebuje vhodnou anténu, přesněji celou mřížku antén.
Kdyby zařízení obsahovalo pouze jednu anténu, mohlo by pouze detekovat, jestli se stylus nachází v jeho blízkosti. Nemohlo by však snímat polohu pera. K tomu je zapotřebí více antén systematicky umístěných ve dvou směrech - na osách X a Y.

Slovem anténa je myšlena cívka, čili smyčka vodiče, kterou prochází elektrický proud. Ten musí být střídavý, jelikož stejnosměrný proud by nerozkmital elektrony a nebylo by možno snímat stylus.

Frekvence střídavého proudu pro EMR digitizér se volí často v rozmezí 500 až 750 kHz, což je rozumný kompromis přinášející jednak dostatečně vysokou frekvenci na rozkmitání cívky ve stylusu a jednak poměrně nízkou hladinu rušení okolními jevy, projevující se převážně u vyšších frekvencí.

Pro lepší vizualizaci je přiložen obrázek 1.

![Obr. 1 Režim vysílání](vysilani.png)

## 2.2 Přijímání

Tato část se stará o detekci zpětně indukovaných elektromagnetických vln ze stylusu. Vykonává tedy měření elektromagnetického pole na jednotlivých cívkách, z jehož naměřených intenzit lze následně aproximovat pozice stylusu na koordinátech X a Y.

Jak již bylo zmíněno na začátku kapitoly, většina zařízení periodicky přepíná mezi režimem vysílání a přijímání. Pro zjednodušení obvodu se však přepíná ještě mezi jednotlivými cívkami. Celá sekvence vysílání a měření tedy probíhá následovně:

1. Zvolení aktivní cívky
2. Spuštění vysílání na dané frekvenci
3. Vypnutí vysílání a zapnutí měření
4. Vypnutí měření a uložení dat
5. Opakování cyklu se zbytkem cívek

Naměřená data se tedy ukládají průběžně pro každou cívku a na konci vysílání a měření ze všech cívek se vypočtou souřadnice pera.

Tento cyklus proběhne ve zlomku sekundy - samotné vysílání trvá pouze v řádu nižších desítek mikrosekund, přijímání taktéž několik mikrosekund a po započtení nutných mezer mezi vysíláním a přijímáním vychází celý cyklus se všemi cívkami přibližně na půl milisekundy ()



[^2]: EMR = elektromagnetická rezonance
