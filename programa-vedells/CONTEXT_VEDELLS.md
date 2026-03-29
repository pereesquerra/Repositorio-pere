# Programa Vedells — Context Complet
## Actualitzat: 29 març 2026 (sessió 3 — v20 avançada)

**Fitxer v19 (FINAL):** factures_vedells_19.html
**Fitxer v20 (WIP):** factures_vedells_20.html
**Carpeta:** /Users/pereesquerra24/Desktop/claude/Webs/programa vedells/
**GitHub:** pereesquerra/Repositorio-pere branca claude/add-claude-documentation-KINri
**Repo:** /Users/pereesquerra24/Desktop/Repositorio-pere
**localStorage:** vd29

---

## REGLA D'OR
El programa MAI esborra animals automàticament. Zero `delete S[g].animals`. Només el granger pot esborrar.

---

## v20 — IMPLEMENTAT

### Sistema IDs interns
- S[g].animals = registre central, S[g]._aidCounter
- nextAid(g), findOrCreateAid(g, dib, data)
- Migració progressiva: crea aids quan s'obre detall/historial/cartilla
- NOMES per entrades (mai sortides)
- Completar si falten (mai resetejar aids existents)

### Fitxa animal (modal z-index:400)
- Clicable des de: detall moviment, historial lots, animals per cartilla, buscador
- Mostra: DIB editable, sexe editable, cartilla, lot, guia, data entrada
- Moviments associats clicables amb fletxa ➤ (fitxaGoMovIdx + lookup table)
- Guardar propaga canvis a TOTS els moviments (crea mv.sexes si falta)
- Refresca detall + cartilla després de guardar

### Buscador d'animals
- Cerca per últims 4 dígits o número complet
- Resultats separats: "A granja" (verd) vs "Sortits" (vermell, amagats per defecte)
- Progressiu: mostra 20 + botó "Mostrar més"
- Separat per granja (seen key: g+'_'+aid)
- estaAGranja() comprova si l'animal ha sortit

### Lots clicables
- "LOT 9 ➤" obre historial (openLotHist)
- CSS: .lc-num amb fons, vora, font gran

### Panell resum granja
- Sobre els lots, grid-column:1/-1
- Total inici→fi + diferència + entrades/sortides mes
- Per cartilla: inici→fi + moviments mes + total entrades lots actius
- Cal millorar disseny mòbil

### 5 dígits
- {1,4} en lloc de {1,5} a TOTES les instàncies
- 5+ dígits: prefix + últims 4

### Sexe
- NOMES editable a entrades (no sortides)
- guardarAnimalFitxa crea mv.sexes si no existeix
- Propaga per aid (no per dib)

---

## PRÒXIMA TASCA: GRANJA "LA COMA"

### Dades
- Nom: ECOFUTUR AGRÍCOLA RAMADER - LA COMA
- Cartilla: 712:AX (abreviatura: COM)
- REGA: ES082290036967
- Color suggerit: marró terra #8B6914

### Requisits
- Pestanya nova independent al costat de Figuera i La Costa
- ~50 vaques + 2 toros + vedells fills
- Lot 100 per defecte
- Entrades, sortides, baixes (igual que Figuera)
- DATA DE NAIXEMENT per animal → edat calculada (anys i mesos)
- GENEALOGIA: camp "Mare" a la fitxa (DIB mare, clicable)
- Facturació desactivada per defecte (opció d'activar)
- Càrrega inicial des d'Excel
- Buscador separat (no barrejar amb Figuera/Costa)
- Molt pocs moviments anuals

### Implementació
1. Afegir 'coma' a defState amb lots, movs, sexes, animals, etc.
2. Afegir pestanya HTML
3. Adaptar renderG, rLots, etc. per 3 granges
4. Camp dataNaix a S[g].animals → edat a fitxa i llistats
5. Camp mare a S[g].animals → link clicable
6. Importador Excel

---

## DADES TÈCNIQUES
- localStorage: vd29
- PDF.js: v3.11.174
- REGA Figuera: ES082290033519
- REGA La Costa: ES081920008093
- REGA La Coma: ES082290036967
- Colors: ECO=#4a7c59, PE=#e06a00, SATF=#7b5ea7, RAM=#3d6b8c, COM=#8B6914
- Preus: pre-2025=0.30, 2025=0.35, 2026+=0.40


---

## BUGS CONEGUTS / PENDENTS (29 març 2026)

### Buscador
- 1.652 animals al Mac quan haurien de ser ~707: duplicats de migracions anteriors bugades
- Fix aplicat: migració ara completa en lloc de resetejar, però els duplicats antics segueixen al localStorage
- Per netejar: localStorage.removeItem('vd29') al Mac i GitHub Pages
- A l'iPhone: esborrar dades de github.io a Safari
- Buscar "????" funciona però mostra massa resultats per duplicats antics

### Panell resum granja
- Al mòbil (iPhone) no es veu bé — massa gran, no s'adapta
- Els números de cartilla poden ser incorrectes si hi ha lots amb vIni sense cartilla assignada
- Cal fer-lo més prim/horitzontal i responsive

### Fitxa animal al mòbil
- Moviments clicables: FUNCIONA amb fitxaGoMovIdx + lookup table (botó natiu)
- Guardar canvis: FUNCIONA des de tots els llocs

### Migracions
- La migració progressiva NOMES crea animals per ENTRADES (no sortides)
- Si m.aids ja existeix, completa els que falten sense resetejar
- findOrCreateAid NO deduplicà ????-???? (cada un és únic)

---

## FLUX DE TREBALL

### Editar fitxer al Mac
1. Desktop Commander: read_file, edit_block, write_file, start_process
2. Filesystem: edit_file (alternativa per edicions exactes)
3. Python scripts via start_process per substitucions complexes

### Verificar JS
```
python3 -c "import re,subprocess;..." (veure CONTEXT anterior)
```
Alternativa: `cd /tmp && node -c check_js.js`

### Pujar a GitHub
```
cd /Users/pereesquerra24/Desktop/Repositorio-pere
cp "...factures_vedells_20.html" programa-vedells/programa_factures_vedells_v20.html
git add -A && git commit -m "msg" && git push origin claude/add-claude-documentation-KINri
```

### Obrir Chrome
```
open -a 'Google Chrome' '/Users/.../factures_vedells_20.html'
```

### iPad/iPhone
```
https://pereesquerra.github.io/Repositorio-pere/programa-vedells/programa_factures_vedells_v20.html?v=N
```
Incrementar ?v=N per forçar refresc caché

---

## DECISIONS D'ARQUITECTURA IMPORTANTS

1. **Un sol fitxer HTML** — tot el CSS, JS i dades en un sol fitxer
2. **localStorage** — les dades es guarden al navegador, no al servidor
3. **defState()** — dades inicials hardcodejades al codi (fallback si localStorage buit)
4. **No esborrar mai** — el programa MAI esborra animals, només el granger
5. **Migració progressiva** — els IDs es creen quan l'usuari consulta vistes, no al carregar
6. **Granges independents** — cada granja té el seu S[g] completament separat
7. **findOrCreateAid** — per DIBs reals busca si existeix; per ????-???? crea sempre un de nou
