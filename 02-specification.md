---
project_outline: "[[00-project/01-project-outline.md]]"
---

# Autunóm roboto szimulációs rendszer

## Szerepkörök és Jogosultságok

| Szerep | Igény | felelőség/hozzáférés |
|---|---|---|
| Kutató/Felhasználó | Kisérletek indítása, robotok viselkedésének kiértékelése | Konfigurálja a pályákat, Tereptárgyak és akadályok elhelyezése, elindítja a tesztelési folyamatot, eredmények letöltése/rendszerezése |
| Ágens(robot) | Környezet feltérképezése akafályok és tárgyak észlelése, feladatok elvégzése, kommunikáció | Interakció a környezettel és a többi Ágensel(ha vannak) és a megadott feladat elvégzése emberi beavatkozás nélkül |

## 2. Use case-ek / user storyk

### Szimulációs kísérlet futatása

- **Szereplő:** Kutató/Felhasználó
- **Előfeltétel:** A kísérlet paramétereinek megadása: Pálya mérete, akadályok és mozgatható tárgyak elhelyezkedése, robotok száma.
- **Fő folyamat:**
1. A felhasználó elinditja a szimulációs felületet.
2. pálya paramétereinek megadása.
3. A backand legenerálja a pályát a megadott adatok alapján.
4. A rendszer elhelyezi az autonóm robotokat.
5. A szimuláció elindul: a robotok érzékelnek kommunikálnak és mozgatnak tárgyakat.
6. Valós időben megjelennek a lépések.
7. A rendszer folyamatosan naplózza az álapotot a komunikációt és a jutalmakat.
8. A feladat elvégzésekor vagy az időkorlát elérésekor befejetődik a szimuláció.
- **Hibafolyamatok:** Ha egy robot át ptobál kaladni a pálya határán vagy nem mozgatható tárgyat probál mozgatni, ilyenkor a poziciolya mozdulatlan marad és büntető pontot kap.
- **Utófeltétel:** A kisérleti eredmények (sikeresség, idő/megtett út, kommunikációs napló) eltárolásra kerülnek és exportálhatók.

## 3. Funkcionális követelmények

| Követelmény | Elfogadási kritérium | Prioritás |
| --- | --- | --- |
| A rendszer képes 2D-s pálya generálására | A kezdetben megadott paraméterek alapján generált pálya tartalmat kezdőpontot akadályokat és cél mezőt. | Kötelező |
| Robot akcióterének megadása | A robot képes legyen 4 irányba mozogni az elmozdítható dobozokat eltolni illetve a többi robotnak üzenetet köldeni. | kötelező |
| Kommunikációs csatorna szimulálása | A robotok jogosultságuknak megfelelően küldhetne, fogadhatnak és lehalgathatnak üzeneteket. | kötelező |
| Ütközések és érvénytelen lépések kezelése | A robotok nem lehetnek egyszerre ugyanazon a mezőn, a falakon nem mehetnek keresztül. | kötelező |
| Legalább két algoritmus csatlakoztatása | A rendszer képes  egy tanuláson alapuló és egy klasszikus útkereső robotot futtatni. | kötelető |
| Kísérleti adatok exportálása | A kisérlet végén a kommunikácios napló és a sikerességi ráta letölthető. | kötelező |
| Vizuális megjelenítés valós időben | A felhasználó valós időben látja a 2D s pályán a robotokat. | Ajánlott |

Prioritás: **Kötelező** = a végtermékhez szükséges; **Ajánlott** = fontos; **Lehetséges** = idő esetén opcionális.

## 4. Üzleti szabályok és korlátok

| Szabály vagy korlát | Indoklás |
| --- | --- |
| Addatok szeparálása tanulás és tesztelés között | Megakadályozza a modellek tultanulását és validálja az általánosítóképességet. |
| Tér és idő | Az MI modellek számára kezelhető méretű és elrendetésű pálya és elegendő idő a feladatvégzésre |
| Determinisztikus környezeti átmenetek | Bár a robotok lépései lehetnek véletlenszerüek de egy irányba elmozdulás mindig ugyanazt a fizikai eredményt kell hozza |
| Hardver komunikációs réteg kihagyása | A feladat központjában a *döntéshozatal* áll nem a hálózatbiztonság vagy a fizikai zavarás |

## 5. Felhasználói felület és munkafolyamat

A rendszer kettő fő nézetből áll. Az első a **Konfigurációs Irányitópult**, itt álithatja be a kutató/felhasználó a pálya méretét, dobozok számát, robotok számát és az algoritmust. A második a **Szimulációs nézet**, amely megjeleníti a 2D-s pályát illetve a dobozokat és a célt. A nézet oldalsó sávjában látható az idő, lépésszám, elért jutalmak száma.

## 6. Nem funkcionális követelmények

| Követelmény | Ellenőrzés módja |
| --- | --- |
| Szabványos MI API kompatibilitás | A környezet implementálja a Gymnasium (korábban OpenAI Gym) vagy PettingZoo (Multi-Agent) interfészt. |
| Kliens szerver kommunikáció késleltetése vizuális módban | WebSockets használata esetén a lépésfrissités vizualizációja folyamatos (min.30 fps) |
| Moduláris kódarchitechtúra | Új felafattípus hozzáadása az alap motor modosítása nélkül (Pl. Összedolgozó robotok helyett versengők legyenek) |

## 7. Nyitott kérdések és kockázatok

| Kérdés/kockázat | Hatás | Feloldás/döntés |
| --- | --- | --- |
| A gépi tanulási algoritmusok betanításí ideje túl hosszú | Befojásolja a kísérlet iterációs sebességét | Egyszerűsített környezet és gyakori jutalmazás használata |
| A kliens és a tanuló algoritmusok összekötése nehéz lehet | Befolyásolja a teszt stabilitását | A szimuláció és a tanulás is úgyanazon a nyelven működik. A webes felület csak megjelenítí a generált naplófájlokat vagy webSocketen át nézőként csatlakozik |
| A kommunikációs tér túl nagyra nőhet | Lehetetlenné teszi a robotok tanulását | Korlátozott diszkrét "szótár" előre megadott 4-8 lehetséges üzenet bevezetése a szöveges kommunikáció helyett |

## 8. Kezdeti technikai javaslat

### Javasolt megoldás

A rendszer magja Phyton szimulációs környezet amely a PettingZoo szabványra épül. Ebbe fut a térkép generálása és a robotok betanítása. A vizualizáció úgy történik, hogy a Phyton motor elmenti a kísérlet eredményeit és a lépések sorozatát amit a weboldalon utolag le tud játszani.

### Megvalósíthatóság és technikai kockázatok

| Kockázat/feltételezés | A korai fázisra tervezett validáció | Tartalék megközelítés |
| --- | --- | --- |
| A backend és a frontend közötti kapcsolat túl lassú az MI számára | Szimuláció futása aszinkron módón | Az élő kapcsolat elhagyása, az MI lefut utána álapotot ment és a webes delületen csak lejátsza a történést |
| A robotok nem tanulják meg a kollaboratív feladatmegoldást(pl doboz együtt tolása) | Kisérlet nagyon kis méretű pályán való validálása egyszerű szabályokkal | A feladatok leegyszerüsítése vagy a hagyományos algoritmusok használata tanulás helyett |
