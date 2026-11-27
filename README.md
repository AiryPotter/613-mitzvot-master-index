# 613 Mitzvot — Master Index (Phase 1)

> **CONFIDENTIAL — DRAFT.** Not yet published. Intended license on release: CC0 1.0 (public domain dedication).

## Files

| File | What it is |
|---|---|
| `data/mitzvot_master_index.csv` | 613 rows, UTF-8, one row per commandment. The master numbering for the guide. |
| `data/pass2/chinukh_links_raw.json` | Unverified Sefaria links from each Rambam number to Sefer HaChinukh numbers. Input for pass 2 only. |
| `README.md` | This file: columns, method, sources, known issues. |

## Numbering

- **Master enumeration:** Maimonides, *Sefer HaMitzvot* (SHM). Order and content follow SHM, **not** the list Maimonides placed at the start of the Mishneh Torah. The two lists order a few commandments differently (see Known issues).
- `guide_no` 1–248 = Positive 1–248 (`P1`–`P248`); `guide_no` 249–613 = Negative 1–365 (`N1`–`N365`).
- **Verse numbering is Hebrew (Masoretic).** This matches the JPS 1917 English. KJV-style English numbering differs in some chapters (e.g., Deut. 23, Ex. 22, Lev. 6).

## Columns

| Column | Meaning |
|---|---|
| `guide_no` | 1–613 |
| `rambam_no` | `P#` (positive) or `N#` (negative), per SHM |
| `type` | Positive / Negative |
| `short_title` | Concise English title, written from SHM's Hebrew definition (not copied from any translation) |
| `verse_cited` | Torah verse(s) whose wording Rambam quotes in SHM; Hebrew numbering |
| `mishneh_torah_ref` | Mishneh Torah section (Sefaria English name) and chapter, or `chapter:halakha` |
| `verse_check` | `verified` = verse wording found in SHM's Hebrew text; `sources agree` = quote not auto-matched, but the Mishneh Torah list, Sefaria links and Glazer agree; `manual` = resolved by reading the Hebrew |
| `mt_ref_source` | `sefaria-link` = curated Sefaria link; `checked` = located by searching the Mishneh Torah Hebrew; `note` = from the 1883 edition's location note only (least certain); `note+checked` = note confirmed in the Hebrew |
| `notes` | Issues found so far (ordering differences, interpretive points, verses needing checks) |
| `sefaria_ref` | Canonical reference for scripts and the Sefaria API |
| `shm_hebrew_definition` | Opening clause of SHM's Hebrew definition (Warsaw 1883, public domain), for checking titles |

## Method (reproducible)

1. **SHM Hebrew text:** *Sefer HaMitzvot*, Warsaw 1883 (Ibn Tibbon's Hebrew translation of the Judeo-Arabic original), Public Domain, via the Sefaria-Export bulk dataset (`json/Halakhah/Sifrei Mitzvot/Sefer HaMitzvot/...`).
2. **Torah text:** "Tanach with Text Only" (Public Domain), via Sefaria-Export.
3. **Verses:** candidate references were taken from three sources: the Mishneh Torah's own list of the 613 (Hyamson translation, 1937–49, PD), Glazer (1927, PD), and curated Sefaria links. A verse was kept only if its Hebrew wording appears in SHM's text for that commandment (shared 3-word or 2-word runs, ignoring vowels and plene/defective spelling). Short citations were trimmed to the verified verses; passage-level citations (more than 3 verses, e.g., the impurity laws) were kept as ranges.
4. **Mishneh Torah references:** curated Sefaria links (573 rows). For the remaining 40 rows, the chapter was located by searching the Mishneh Torah Hebrew, or taken from the edition's location note.
5. **Titles:** written fresh from SHM's Hebrew definitions; the PD Hyamson list was used as a guide.

Bulk data came from the public bucket `gs://sefaria-export`, as Sefaria asks AI agents to do. No copyrighted or non-commercial (CC-BY-NC) text is reproduced. Verse and chapter references are facts.

## Known issues / for later passes

- **Ordering differences between SHM and the Mishneh Torah's own list:** P17/P18, N167/N168, N295/N296, N327–N329. SHM order is used. Each is flagged in `notes`. Sefaria's links also follow the Mishneh Torah list for P17/P18.
- **P43:** Rambam's quoted wording matches Lev. 23:36 (a Sukkot verse). The Passover verse is Lev. 23:8 / Num. 28:19. Needs review.
- **P6:** the verse says "cleave to Him"; SHM explains it as associating with Torah scholars.
- **Derived prohibitions** with no explicit verse: N135 and N336 (flagged).
- **Rows with `mt_ref_source = note`** (10) should be confirmed against the Mishneh Torah text.
- **Pass 2:** add a Sefer HaChinukh number column. `chinukh_links_raw.json` covers 607 of 613 rows; 4 rows have two candidates (P107, N83, N121, N328). Verify against the Chinukh text (Nataf English translation, CC0).
- **Enumeration notes** (Halakhot Gedolot, Ramban, Semag, etc.) are not yet included. See the planned entry template.

## License

CC0 1.0 Universal (public domain dedication). See [`LICENSE`](LICENSE).

All source texts used are public domain. The files contain no copyrighted translations.
