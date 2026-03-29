# CONTEXT VEDELLS — Actualitzat 29/03/2026

## FITXERS
- **v20 (ACTUAL):** `factures_vedells_20.html` (265KB) — amb La Coma
- **v19:** `factures_vedells_19.html` (185KB) — última sense La Coma
- **v18:** `factures_vedells_18.html` (74KB)
- **v17:** `factures_vedells_17.html` (73KB)
- **GitHub:** `pereesquerra/Repositorio-pere` branca `claude/add-claude-documentation-KINri`
- **Carpeta local:** `/Users/pereesquerra24/Desktop/claude/Webs/programa vedells/`
- **localStorage key:** `vd29`

## TRES GRANGES

### Figuera (fig)
- Cartilles: ECO, SATF, PE
- Gestió per VOLUM (sense DIBs individuals)
- Animals: `????-????` (placeholders)
- NO té: mare, fills, dataNaix, raça, morfotip

### La Costa (costa)
- Cartilla: RAM
- Gestió per VOLUM
- Animals: `????-????` (placeholders)
- NO té: mare, fills, dataNaix, raça, morfotip

### La Coma (coma) — NOU v20
- Cartilla: COM (COM 712:AX)
- REGA: ES082290036967
- Color: #8B6914 (marró terra)
- Gestió per ANIMAL INDIVIDUAL amb DIBs reals
- **69 animals** importats del GTR (25 FR + 44 ES)
- Lot 100 (únic lot actiu)
- Migració flag: `_v3` (s'executa una sola vegada)
- `syncComaLot()` sincronitza lot.v amb animals reals

#### Dades per animal (NOMÉS La Coma)
- DIB, sexe, dataNaix, morfotip/raça
- Mare (NOMÉS per ES, no per FR — les mares FR són a França)
- Fills: historial de parts complet (99 parts de 36 vaques, des de 2021)
- Tipus: Vaca (♀ ≥2 anys), Toro (♂ ≥2 anys), Vedell/a (<2 anys)

#### Fitxa animal
- Mode CONSULTA per defecte (res editable)
- Botó "✏️ Editar" per entrar en mode edició
- Mode edició: DIB, dataNaix, mare, sexe (♀/♂/—), + botó 🗑 Eliminar
- Eliminar: confirmació amb info lot/sexe/dib + avís botó ↩ Desfer
- Mare fora explotació: badge vermell "Fora explotació" (no clicable)

#### Layout La Coma (ordre visual)
1. Header + Lots actius (Lot 100) + botons
2. Moviments del mes (calendari `<input type="date">`)
3. Comptadors (Vaques/Toros/Vedells/Total)
4. Llistat d'animals (desplegables per categoria)
5. Notes, Historial lots, Animals per cartilla, Importar CSV

## FUNCIONALITATS IMPLEMENTADES v20

- Tres pestanyes: Figuera, La Costa, La Coma
- Panell resum granja amb nom+color correcte per cada granja
- DIBs clicables als moviments (busca per DIB al registre)
- Modal dades extra per nous animals La Coma (raça, dataNaix, sexe, tipus, mare)
- Modal confirmació es tanca ABANS de renderG (no duplica animals)
- Mare/fills/raça/naixement EXCLUSIUS de La Coma (eliminat de Figuera/Costa)
- Adjuntar PDF per entrades La Coma
- Lot 100 sempre visible (condició `g==='coma'&&l.actiu&&l.v>0`)

## BUGS RESOLTS v20
- `_hist` temporal dead zone: migracions usen `localStorage.setItem()` directe
- `_hiddenLots` sense entrada `coma`: afegit `coma:new Set()`
- Modal confirmació no es tancava: `closeMD()` cridat abans de `renderG()`
- Panell "La Costa" a La Coma: afegit `g==='coma'?'La Coma':...`
- Animals nous no apareixien: `rComaResum` ara inclou animals sense dataNaix

## PENDENTS
- Calendari per data d'incorporació al formulari entrada
- Adjuntar PDF per entrades vedells (parse DIBs del PDF)
- Preguntar raça + tipus al fer entrada manual
- Login + multi-granja (Supabase Auth)
- PWA instal·lable
- Deploy a gesclic.com

## DADES LA COMA (origen)
- `ImpressioDIBsXLS-4.xls` — DIBs, sexe, morfotip, dataNaix
- `Document_DIBs-7.pdf` — Mare de cada animal, data incorporació
- `LlistatNaixementsXLS 20260329082048.xlsx` — 129 naixements (2021-2026), historial parts
- Carpeta: `/Users/pereesquerra24/Desktop/LA COMA/`

## COM CONTINUAR
Frase per iniciar nova sessió:
> Llegeix CONTEXT_VEDELLS.md i factures_vedells_20.html. Continuem amb la v20.
