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

