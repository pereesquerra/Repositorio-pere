# Programa Vedells — App Gestió Animals Boví
## Context del Projecte

**Propietari:** Pere Esquerrà — Abatt Associats SL  
**Domini:** gesclic.com + gesclic.es (comprats a Dinahosting, març 2026)  
**Repositori GitHub:** pereesquerra/Repositorio-pere  
**Branca activa:** claude/add-claude-documentation-KINri  
**App actual:** programa-vedells/programa_factures_vedells_v18.html  
**URL pública:** https://pereesquerra.github.io/Repositorio-pere/programa-vedells/programa_factures_vedells_v18.html  
**Pàgina principal:** https://pereesquerra.github.io/Repositorio-pere/  

---

## ESTAT ACTUAL (març 2026)

### App existent (v18)
- Fitxer HTML+JS pur, 76KB
- localStorage key: 'vd29'
- Gestiona animals per VOLUM (no per individu)
- Dues granges: Figuera + La Costa
- Facturació automàtica per cartilla/empresa
- Preu editable per empresa/cartilla (pastilla clicable)
- Càlcul: dies × animals × preu (0.40€/dia per defecte)

### Les dues granges

**Granja Figuera (Sant Mateu de Bages)**
- Cartilles: ECO (Ecofutur, verd #4a7c59), SATF (SAT Figuera, lila #7b5ea7), PE (Pere Esquerrà, taronja #e06a00)
- Lots actius: Lot 9 (257 vedells: 203 ECO + 54 PE), Lot 10 (54 SATF)
- Des de 2026: Factura separada per cartilla (IC{m}/{y}, SAT{m}/{y}, PE{m}/{y})

**Granja La Costa (Santpedor)**
- Cartilla: RAM (Ramaders Comarcals, blau #3d6b8c)
- Lots actius: 25-28
- Una sola factura mensual

### Regles de facturació CRÍTIQUES
- Dia entrada: ES COBRA
- Dia sortida: ES COBRA
- Fórmula: Animals × Dies × Preu
- Cross-billing: si cartilla s'esgota, excedents van a altra cartilla
- Un lot apareix si tenia animals o entrades aquell mes

---

## MIGRACIÓ PLANIFICADA: Volum → Individu

### Estructura actual del moviment
```javascript
{dia, tipus, qty, lot, cart}
```

### Nova estructura del moviment (v19+)
```javascript
{
  dia: 15,
  tipus: 'entrada',  // entrada | sortida | baixa
  lot: 9,
  cart: 'ECO',
  dibs: ['ES123456789', 'ES987654321'],  // nums individuals (crotals)
  guia: '92507011000293790',  // número de guia sanitària OBLIGATORI
  qty: 2  // calculat automàticament = dibs.length
}
```

---

## LLISTA DE FUNCIONALITATS A IMPLEMENTAR

### Fase 1 — Millores sobre v18 (HTML pur)
1. ~~Preu editable per factura~~ ✅ FET (v18)
2. Buscador per últimes 4 xifres del crotal (DIB)
3. Entrada massiva DIBs — separats per comes O números llargs (discriminació automàtica)
4. Número de guia sanitària — camp a entrades i sortides, mostrat al llistat
5. Apartat cuidador — vista sense preus
6. Apartat propietari — vista completa amb facturació

### Fase 2 — Arquitectura nova (gesclic.com)
1. Login usuaris — Supabase Auth (email/password)
2. Multi-granja per usuari
3. Rols: Propietari (tot) vs Cuidador (granja assignada, sense preus)
4. PWA instal·lable a iPhone/Android sense App Store
5. Stack: Cloudflare DNS → Hostinger (hosting) + Supabase (dades+auth)

### Fase 3 — Funcionalitats avançades
1. OCR de guies sanitàries (PDFs digitals i escaneig paper)
2. Historial complet per animal individual (crotal)
3. App mòbil simplificada per treballadors

---

## INFRAESTRUCTURA

- **Mac de treball:** iMac 24" — usuari: pereesquerra24
- **Carpeta local:** /Users/pereesquerra24/Desktop/claude/Webs/programa vedells/
- **Fitxer local app:** /Users/pereesquerra24/Desktop/claude/Webs/programa vedells/factures_vedells_18.html
- **Referència tècnica:** /Users/pereesquerra24/Desktop/claude/Webs/programa vedells/CONTEXT_VEDELLS.md
- **Hosting:** Hostinger (ja pagat)
- **DNS:** Cloudflare (gratuït)
- **BD + Auth:** Supabase (pla gratuït)
- **Domini:** gesclic.com + gesclic.es (Dinahosting)

---

## MODEL DE NEGOCI (futur)

- Producte: App gestió ramadera vendible a tercers
- Preu: 9.90€ cop únic (sense quotes mensuals)
- Dades: Al Google Drive/Supabase de l'usuari
- Canal: TikTok/Instagram Reels + descàrrega directa

---

## COM TREBALLAR AMB CLAUDE CODE

Cada sessió:
```bash
cd "/Users/pereesquerra24/Desktop/claude/Webs/programa vedells"
claude
```
Primera ordre: "Llegeix CONTEXT_VEDELLS.md i factures_vedells_18.html i continuem el projecte Programa Vedells"

Al final de cada sessió important: "Actualitza el CLAUDE.md amb el que hem fet avui i puja'l a GitHub"

---

## NOTES TÈCNIQUES

- Colors: ECO=#4a7c59, PE=#e06a00, SATF=#7b5ea7, RAM=#3d6b8c
- Fonts: DM Sans + Playfair Display + DM Mono
- IMPORTANT: Evitar backticks niuats en template literals JavaScript
- Els guies sanitàries al camp 'guia' son strings (ex: '92507011000293790')
