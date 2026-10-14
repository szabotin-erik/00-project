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
3. 