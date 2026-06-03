# Warmtenet-tool — VIVET-warmtevraagdata (heel NL)

Per-gemeente JSON met het **referentieverbruik warmte** per woning, gekeyd op
**BAG-verblijfsobject-identificatie** (`vbo_id`). Wordt door de Warmtenet-tool
opgehaald bij de BAG-gebiedsimport en op `vbo_id` aan de BAG-panden gekoppeld.

- **352 gemeenten · ~7,06 miljoen woningen** · ~686 MB.
- Bestand per gemeente: `GM<CBS-gemeentecode>.json` (bv. `GM1942.json` = Gooise Meren).

## Bron

PBL/CBS — **VIVET "Referentieverbruik warmte woningen II (2025)"**
(<https://dataportaal.pbl.nl/VIVET/Referentieverbruik_warmte_woningen_II_2025>).
Open data; modelmatige schatting van de warmtevraag o.b.v. bouwtechnische kenmerken.
**Woningen-only** — utiliteit zit hier niet in (de tool valt daarvoor terug op kentallen).

## Formaat

```json
{ "gemeente": "1942", "bron": "VIVET …", "n": 27343,
  "byVbo": { "0424010000000050": { "rv": 48.2, "tw": 4.9, "gas": 54.1,
    "op": 103, "wt": 2, "bp": 1, "bj": 1931, "eg": 0, "lb": "x" } } }
```

Velden: `rv` ruimteverwarming-GJ · `tw` warm tapwater-GJ (rvtw = rv+tw) · `gas` aardgas-GJ ·
`op` m² · `wt` woningtype 1–5 (VIVET 6→5) · `bp` bouwperiode 0–11 · `bj` bouwjaar ·
`eg` eigendom 0/1/2 · `lb` energielabel A–G/x.

## Opnieuw genereren

In de tool-map (`download_vivet.py` + `vivet_to_json.py`):

```sh
python3 download_vivet.py vivet_csv/          # alle gemeente-CSV's van het PBL-dataportaal
python3 vivet_to_json.py vivet_csv/ -o vivet/ # → GM<code>.json
```

## Gebruik in de tool

Zet `VIVET_BASE_URL` in `Warmtenet-tool.html` op de GitHub-Pages-URL van deze map,
bv. `https://<gebruiker>.github.io/warmtenet-vivet/`.
