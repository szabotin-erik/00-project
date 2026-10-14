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

