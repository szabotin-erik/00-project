---
project_outline: "[[00-project/01-project-outline]]"
---

# Többrobotos autonóm feladatmegoldás vizsgálata szimulált környezetben

Szerző: Szabotin Erik
Neptun: V4XBUU
Témavezető: Storcz Tamás
Projektazonosító: 2026-ST-03

## Probléma

- **Fizikai megvalósítás nehézségei:** Ha valós fizikai robotokkal szerettnénk algoritmusokat és MI ágenseket tesztelni az kölcséges és lassú lenne plusz hardveres meghibásodás torzithatja a vizygálat eredményeit.
- **Reprodukálhatóság:** Valós környezetben a fizikai tényezők befolyásolhatják a teszt kimenetelét.
- **Döntéshozatal megfigyelése:** Robotok interakciojának és kommunikációjának kiértékelése.
- **Összehasonlíthatóság:** Az útkereső algoritmusok és a gépi tanulásra épülő modellek teljesítményének mérése azonos paraméterek mellet.

## Célfelhasználók

1. **Kutató / Felhasználó**

- **Cél:** Kísérletek konfigurálása és indítása robotok vizselkedésének és sikerességének vizsgálata.
- **Feladatok:** 2D pálya mérete, akadályok helye illetve a start és cál mezők elhelyezése. Eredmények kiértékelése.

2. **Robot**
 
- **Cél:** A feladat elvégzése emberi beavatkozás nélkül.
- **Képességek:** Környezet feltérképezése, akadályok érzékelése, tárgyak mozgatása és kommunikáció a többi robottal ("szótár").

## Tervezett hatókör

### Benne van 

- 2D-s paraméterezhető pálya generálása
- Robotok akcióterének(mozgásának) modellezése
- Kommunikácios csatorna szimulálása
- Kísérlet eredményeinek exportálása és webes vizualizációja

### Nincs benne

- Valós fizikai robotokal történő tesztelés
- Kommunikácios csatorna fizikai jeltorzításának, zavarásának szimulálása
- 3D-s grafikus megjelenítés

## Kezdeti felhasználói utak

1. **Paraméterezés**

- Pálya mérete, dobozok/falak elhelyezése, célpont, robotok számának beállítása algoritmus kiválasztása

2. **Szimuláció futtatása**

- Robotok elhelyezése és cselekvés kezdete
- A szabályok szigorú vizsgálata, büntetőpontok és jutalmak
- lépésszám jutalmak és a hátra lévő idő folyamatos frissítése/megjelenítése

3. **Adatkinyerés:**

- A feladat sikeres elvégzése, határidő lejártakor szimuláció lezárása
- Az állapotváltozások, a kommunikácós napló exportálása

