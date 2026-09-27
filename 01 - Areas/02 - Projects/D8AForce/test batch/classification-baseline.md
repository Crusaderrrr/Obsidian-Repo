# Classification baseline — configuration, expected results, data ownership

Reference for regression-testing the classifier after an algorithm change or a reference-data
re-parse. Self-contained: the fixture rows are embedded below.

---

## 1. CS STEPS configuration

Captured 2026-08-14. Results are only comparable across runs while this is unchanged — a
threshold edit moves rows on its own and looks exactly like a code regression.

| Search Step | Threshold | Lastname Threshold | Enabled |
|---|---|---|---|
| CFA Search | 0.75 | 0.67 | yes |
| CRD Search | 0.80 | 0.80 | yes |
| Residential Address Search | 0.70 | 0.90 | yes |
| CSA Search | 0.90 | 0.90 | yes |
| FCA Search | 0.50 | 0.50 | yes |
| Occupation Verification | 0.90 | 0.90 | yes |
| IMCA Search | 0.50 | 0.50 | yes |
| SEC Search | 0.80 | 0.80 | yes |
| Entity Name Search | 0.80 | 0.80 | yes |
| NFA Search | 0.80 | 0.80 | yes |
| SFC Search | 0.90 | 0.50 | yes |
| Company threshold for CRD, NFA, SEC, CFP and CSA | 0.80 | 0.80 | yes |
| CFP Search | 0.70 | 0.70 | yes |
| Email Search | 0.90 | 0.50 | yes |
| Email Search (Username match) | — | — | yes |
| Email Search (Domain match) | — | — | yes |
| Email Username Patterns Search | 0.60 | 0.50 | yes |

### Where these thresholds actually apply

- **The company threshold replaces the per-step threshold** for CRD, NFA, SEC, CFP and CSA
  whenever the company step is enabled — 0.80 everywhere in this snapshot.
- **Name matching on the pro path ignores these thresholds** for SEC / CRD / CFP / CSA. The pro
  branch requires `strongMatch()`, an exact 1.0 after lowercase and trim. Thresholds govern the
  gray list and the company score only.
- **CFA** uses the step threshold for first name (0.75) and the lastname threshold (0.67) in
  `basicFilter`, then requires state, city or country agreement.
- **Distance never blocks a pro result** for CRD / SEC / CFP. `defineAndSetProInvestor` does not
  consult it; it only appears in `isNonProfessionalInvestor`, deciding NON_PRO vs UNKNOWN.
- **FCA Search is configured but never runs.** `FCASearchStep` is not registered in
  `ClassifierAlgorithm`, so its threshold has no effect on any result. Same for
  `ZipCodeSearchStep`.

### Rows in this screen that have no effect

Neither the step nor its evidence reads a threshold, so changing these values changes nothing:

| Row | Configured | What actually decides the result |
|---|---|---|
| IMCA Search | 0.50 / 0.50 | `numberOfProfiles == 1` → PRO, `> 1` → UNKNOWN |
| Residential Address Search | 0.70 / 0.90 | PostGrid `isValid` / `isResidential` |
| Email Username Patterns Search | 0.60 / 0.50 | `prefixType == COMMERCIAL_PREFIX`, exact enum match |
| FCA Search | 0.50 / 0.50 | nothing — step not registered in the algorithm |

Partly overridden:

- **CSA 0.90 / 0.90** — names use `strongMatch` (exact 1.0), company uses the 0.80 Company
  override, so CSA's own values are unused while Company search is enabled.
- **Email Search lastname 0.50** — email scores use the `EMAIL_PREFIX` parameter, so
  `getLastNameThreshold` is never consulted. Only the 0.90 applies.

Load-bearing: CFA 0.75/0.67, CRD 0.80/0.80, SEC 0.80/0.80, NFA 0.80, Occupation 0.90,
Entity Name 0.80, SFC 0.90/0.50, Company 0.80, Email 0.90.

---

## 2. Result precedence

```
PROFESSIONAL      if ANY step returns pro
UNKNOWN           else if ANY step returns unknown
NON_PROFESSIONAL  else
```

A disabled step contributes no evidence rather than a non-pro vote. Because pro wins outright,
any row with a predicted pro step has an expected result independent of every other step.

## 3. Country gate

| Country | Steps executed | Count |
|---|---|---|
| USA | EntityName, ResidentialAddress, Occupation, SEC, CRD, NFA, CFA, IMCA, Custom, Email, EmailCommercialPrefix, CFP | 12 |
| CANADA | EntityName, ResidentialAddress, Occupation, CFA, CSA, IMCA, Custom, Email, EmailCommercialPrefix | 9 |
| CN | EntityName, Occupation, CFA, SFC, IMCA, Custom, Email, EmailCommercialPrefix | 8 |
| UNKNOWN | EntityName, ResidentialAddress, Occupation, CFA, IMCA, Custom, Email, EmailCommercialPrefix | 8 |
| UK / OTHER | EntityName, Occupation, CFA, IMCA, Custom, Email, EmailCommercialPrefix | 7 |

Country comes from `AddressUtils.getCountry`: empty Country **and** State length ≠ 2 → UNKNOWN;
otherwise first region file matching lowercased Country or uppercased State; else OTHER.

---

## 4. Expected vs actual results

Predictions were derived from the reference data in `parsed_data/` plus the configuration above.
Actuals are from **Batch #366** (`export.csv`) — 32 records in 29 s, run against local Postgres
with `name_search` seeded from dev.

**Run totals: 11 PROFESSIONAL · 2 NON_PROFESSIONAL · 17 UNKNOWN · 2 ERROR**

Note the runtime config had `EMAIL_SEARCH`, `EMAIL_COMMERCIAL_PREFIX_SEARCH`, `CUSTOM_SEARCH`,
`FCA_SEARCH` and `ZIP_CODE_SEARCH` **disabled** (see section 1), so TC23–TC26 never exercised
their intended branch.

| Case | Predicted | Actual | Driving step verdicts | |
|---|---|---|---|---|
| TC01 | PROFESSIONAL | **PROFESSIONAL** | CFA=PRO | ✓ |
| TC02 | PROFESSIONAL | **PROFESSIONAL** | CFA=PRO | ✓ |
| TC03 | UNKNOWN | **UNKNOWN** | CFA=NON_PRO (state gate works), RA=UNKNOWN | ✓ |
| TC04 | UNKNOWN | **UNKNOWN** | CFA=UNKNOWN, SEC=UNKNOWN, CRD=UNKNOWN | ✓ |
| TC05 | PROFESSIONAL | **PROFESSIONAL** | CFA=PRO, CSA=UNKNOWN | ✓ |
| TC06 | PROFESSIONAL | **PROFESSIONAL** | CFA=PRO (empty-state gate confirmed) | ✓ |
| TC07 | PROFESSIONAL | **PROFESSIONAL** | CFA=PRO | ✓ |
| TC08 | PROFESSIONAL | **PROFESSIONAL** | CFA=PRO, SFC=NON_PRO | ✓ |
| TC09 | PROFESSIONAL | **PROFESSIONAL** | SEC=PRO, CRD=PRO | ✓ |
| TC10 | PROFESSIONAL | **PROFESSIONAL** | SEC=PRO, CRD=PRO | ✓ |
| TC11 | UNKNOWN | **UNKNOWN** | CRD=UNKNOWN | ✓ |
| TC12 | UNKNOWN | **UNKNOWN** | CRD=NON_PRO — distance branch confirmed | ✓ |
| TC13 | PROFESSIONAL | **UNKNOWN** | SEC=**NON_PRO** | ✗ |
| TC14 | PROFESSIONAL | **PROFESSIONAL** | SEC=PRO, CRD=PRO | ✓ |
| TC15 | UNKNOWN | **UNKNOWN** | SEC=NON_PRO (predicted UNKNOWN), RA=UNKNOWN | ~ |
| TC16 | PROFESSIONAL | **UNKNOWN** | SEC=**NON_PRO** | ✗ |
| TC17 | gated | **UNKNOWN** | CFP=NON_PRO, CRD=UNKNOWN | ✓ |
| TC18 | gated | **UNKNOWN** | CFP=NON_PRO, RA=UNKNOWN | ✓ |
| TC19 | PROFESSIONAL | **PROFESSIONAL** | Occupation=PRO | ✓ |
| TC20 | PROFESSIONAL | **PROFESSIONAL** | Occupation=PRO, CFA=PRO (accidental match) | ✓ |
| TC21 | gated | **UNKNOWN** | Occupation=NON_PRO, CRD=UNKNOWN | ✓ |
| TC22 | PROFESSIONAL | **UNKNOWN** | Occupation=**NON_PRO** — CEO path did not fire | ✗ |
| TC23 | PROFESSIONAL | **NON_PROFESSIONAL** | all steps NON_PRO; email step disabled | ✗ |
| TC24 | UNKNOWN | **UNKNOWN** | RA=UNKNOWN only; email step disabled | ~ |
| TC25 | UNKNOWN | **UNKNOWN** | RA=UNKNOWN only; email step disabled | ~ |
| TC26 | gated | **UNKNOWN** | RA=UNKNOWN | ✓ |
| TC27 | gated | **UNKNOWN** | RA=UNKNOWN — address did not validate | ✓ |
| TC28 | UNKNOWN | **UNKNOWN** | RA=UNKNOWN | ✓ |
| TC29 | UNKNOWN | **UNKNOWN** | EntityName=**NON_PRO**, RA=UNKNOWN | ~ |
| TC30 | gated | **ERROR** | excluded by `isValid` — blank Country | — |
| TC31 | gated | **NON_PROFESSIONAL** | "Cleared"; OTHER skips the address step | ✓ |
| TC32 | gated | **ERROR** | excluded by `isValid` — blank Country | — |

**20 of 24 firm predictions correct.** All 9 predicted UNKNOWN outcomes hit; 11 of 15 predicted
PROFESSIONAL hit.

### Divergences

- **TC13 / TC16 — SEC returned NON_PROFESSIONAL, not PRO.** `NON_PRO` from SEC means no candidate
  reached a full-name `strongMatch`, i.e. an empty or non-matching result set. Every SEC row that
  *did* succeed (TC09/TC10/TC14) also matched CRD. Verify `GREGORY VAN KESTEREN` and
  `JOSEPH DIGIAMMO` exist in the local `sec_investors` with a `sec_connector` → `sec_companies`
  link; a missing company link zeroes the company score.
- **TC22 — the CEO employer path did not fire.** `CAPITAL PLANNING PARTNERS` scored below 0.90
  against the `CAPITAL PLANNING` term.
- **TC23 — reached NON_PROFESSIONAL for the wrong reason.** The email step was disabled, so it is
  non-pro by absence rather than by the seeded `xrtp.com` domain. It is nonetheless one of only
  two rows that can reach NON_PROFESSIONAL at all.
- **TC15 / TC29 — right overall answer, wrong step.** SEC returned NON_PRO rather than UNKNOWN;
  EntityName recognised `ACME HOLDINGS LLC` as a name (NON_PRO) rather than flagging it. Both rows
  are UNKNOWN only because of the address step.

### Systemic observations

1. **Residential Address is the single largest driver of Gray.** `RESIDENTIAL_ADDRESS_SEARCH` is
   UNKNOWN on every US/Canada row except TC23 — PostGrid rejects the synthetic street addresses.
   Replacing them with real, validatable addresses would move much of the 17 into NON_PROFESSIONAL.
2. **Only two rows can currently reach NON_PROFESSIONAL** — TC23 (address validates as residential)
   and TC31 (OTHER country, so the address step never runs).
3. **The Pro set is reproducible.** Batches #365 and #366 produced the same 11 PROFESSIONAL rows
   despite different `name_search` state. That set is the reliable regression anchor.
4. **TC30 and TC32 never classify.** `AlgorithmScheduler.isValid` requires non-empty FirstName,
   LastName *and* Country; both are routed to `processInvalidRecord`, stamped `ERROR` in Custom2,
   and produce no classification. The fixture therefore has 30 live rows, not 32.
5. **IMCA and SFC are failing silently.** IMCA throws `SocketException: Connection reset` on every
   record and SFC returns HTTP 405 from `apps.sfc.hk`; both are caught and recorded as
   NON_PROFESSIONAL, indistinguishable from a genuine zero-result search.

### Excel damage in this run

`export.csv` shows postal codes with leading zeros stripped (`06498`→`6498`, `07960`→`7960`,
`02726`→`2726`, `02108`→`2108`, `06901`→`6901`, `00000`→`0`) and commas removed from employer
names (`PRIVATE ADVISOR GROUP, LLC` → `PRIVATE ADVISOR GROUP LLC`). Keep the fixture out of Excel
or quote those fields; zip damage silently disables the distance gate.

---

## 5. Fixture rows

Header names are the Jackson bindings on `InvestorBasic`. Note `emailAddress` is the only
lowercase-initial header.

```csv
FirstName,MiddleName,LastName,Address1,Address2,City,State,PostalCode,Zip,Country,Employer,Occupation,Title,emailAddress,Custom1,Custom2,Custom3
William,A,Levant,120 Gilmer Ave,,TALLASSEE,AL,36078,,US,,,,,TC01_CFA_UNIQUE_STATE_CODE,,
John,Adams,Shirts,500 E Main St,,MESA,ARIZONA,85201,,US,,,,,TC02_CFA_UNIQUE_STATE_FULLNAME,,
Alan,F,Willenbrock,900 N Stone Ave,,TUCSON,TX,78701,,US,,,,,TC03_CFA_STATE_MISMATCH,,
David,,Lee,350 5th Ave,,NEW YORK,NY,10118,,US,,,,,TC04_CFA_MULTIPLE_ENTRIES,,
Eugene,A,Hochachka,10250 101 St NW,,EDMONTON,AB,T5J 3P4,,CA,,,,,TC05_CFA_CANADA_PROVINCE,,
Grigor,,Abaryan,1 Poultry,,LONDON,,EC2R 8EJ,,UK,,,,,TC06_CFA_UK_NO_STATE,,
Mark,E,Koznarek,1 Shennan Rd,,SHENZHEN,GUANGDONG,518000,,CN,,,,,TC07_CFA_CHINA,,
Shai,A,Joory,8 Finance St,,HONG KONG,,,,HK,,,,,TC08_CFA_HONGKONG_SFC,,
LARRY,LEE,BRIGHT,36 WESTBROOK PLACE,,WESTBROOK,CT,06498,,US,BRIGHT ASSET MANAGEMENT,,,,TC09_CRD_PRO_EXACT,,
SCOTT,ANDREW,TREVETHAN,1717 ARCH STREET,,PHILADELPHIA,PA,19103,,US,"JANNEY MONTGOMERY SCOTT LLC",,,,TC10_CRD_PRO_WITH_MIDDLE,,
Melinda,,Ollenborger,8515 E ORCHARD ROAD,,GREENWOOD VILLAGE,CO,80111,,US,Acme Widgets Incorporated,,,,TC11_CRD_EMPLOYER_MISMATCH_NEAR,,
Agnieszka,,Valenta,1200 5th Ave,,SEATTLE,WA,98101,,US,Northgate Textiles Limited,,,,TC12_CRD_EMPLOYER_MISMATCH_FAR,,
GREGORY,REGINALD,VAN KESTEREN,1 Speedwell Ave,,MORRISTOWN,NJ,07960,,US,"PRIVATE ADVISOR GROUP, LLC",,,,TC13_SEC_PRO_EXACT,,
ANDREW,,JENKINS,880 Carillon Pkwy,,SAINT PETERSBURG,FL,33716,,US,"RAYMOND JAMES FINANCIAL SERVICES ADVISORS, INC",,,,TC14_SEC_PRO_NO_MIDDLE,,
ALAX,,GITTLER,1000 Harbor Blvd,,WEEHAWKEN,NJ,07086,,US,,,,,TC15_SEC_NO_EMPLOYER,,
JOSEPH,MICHAEL,DIGIAMMO,100 County St,,SOMERSET,MA,02726,,US,JMD FINANCIAL PLANNING INC.,,,,TC16_SEC_REF_ZIP_EMPTY,,
Henry,P,Cerruti,400 Market St,,PHILADELPHIA,PA,19106,,US,,,,,TC17_CFP_NAME_ANCHOR,,
Bryse,Dalton,Cirjak,200 W Adams St,,CHICAGO,IL,60606,,US,,,,,TC18_CFP_NAME_ANCHOR_2,,
Daniel,,Harper,742 Oak Ridge Ln,,COLUMBUS,OH,43215,,US,,ACCOUNTANT,,,TC19_OCCUPATION_SUITABLE,,
Laura,,Bennett,88 Crescent Dr,,DENVER,CO,80202,,US,,,FINANCIAL ADVISOR,,TC20_OCCUPATION_SPECIAL,,
Marcus,,Whitfield,15 Pine Hollow Rd,,PORTLAND,OR,97205,,US,,ACTOR,,,TC21_OCCUPATION_EXCLUSION,,
Priya,,Raghavan,410 Lakeside Ct,,AUSTIN,TX,78701,,US,CAPITAL PLANNING PARTNERS,,CEO,,TC22_OCCUPATION_CEO_EMPLOYER,,
Thomas,,Okafor,55 Cedar St,,BOSTON,MA,02108,,US,,,,t.okafor@xrtp.com,TC23_EMAIL_SEEDED_DOMAIN,,
John,,Smith,12 Elm St,,MADISON,WI,53703,,US,,,,john.smith@gmail.com,TC24_EMAIL_USERPREFIX_FREEDOMAIN,,
Karen,,Delgado,600 Grand Ave,,PHOENIX,AZ,85004,,US,,,,info@northwind-example.com,TC25_EMAIL_COMMERCIAL_PREFIX,,
Robert,,Nakamura,77 Willow Way,,SEATTLE,WA,98109,,US,,,,not-an-email,TC26_EMAIL_INVALID_SKIPPED,,
Emily,,Vasquez,1745 Chestnut Ave,,NASHVILLE,TN,37203,,US,,,,,TC27_ADDRESS_RESIDENTIAL,,
Peter,,Lindqvist,999999 Nowhere Rd,,ZZZZZ,ND,00000,,US,,,,,TC28_ADDRESS_INVALID,,
ACME HOLDINGS,,LLC,80 Corporate Blvd,,STAMFORD,CT,06901,,US,,,,,TC29_ENTITYNAME_NOT_A_NAME,,
Anna,,Kowalczyk,5 Rynek Glowny,,KRAKOW,XYZ,31042,,,,,,,TC30_COUNTRY_UNKNOWN,,
Lukas,,Brandt,12 Konigsallee,,DUSSELDORF,NW,40212,,Germany,,,,,TC31_COUNTRY_OTHER,,
Sofia,,Marchetti,,,,,,,,,,,,TC32_MINIMAL_NAME_ONLY,,
```

---

## 6. What the gated rows depend on

Three inputs outside the reference export decide every row that has no pro step:

1. **`name_search` contents** — Check Search Name reads it. If empty, every row returns UNKNOWN
   from that step and no gated row can ever reach NON_PROFESSIONAL.
2. **PostGrid** — Residential Address is a live call. Synthetic street addresses will usually come
   back invalid ⇒ UNKNOWN, which alone pushes gated USA / CANADA / UNKNOWN rows to UNKNOWN.
3. **IMCA** — a live scrape that runs for *every* country and returns PRO on exactly one profile
   found. A common name can flip any gated row to PROFESSIONAL between runs.

Steps calling live third parties: IMCA and SFC (HTML scraping), NFA (REST), Residential Address
(PostGrid), plus zip-code distance (SmartyStreets, cached in `zip_code`). Single-row moves on
those are suspect before they are regressions.

---

## 7. Database and table ownership

The code names the two datasources `userdata` and `serverdata`; the physical database names come
from environment variables (`EnvUtils.getUserdataEndpoint()` / `getServerdataEndpoint()`), so they
are not visible in the source. On **dev** they resolve as:

| Datasource | Dev database | Access path | Wired in |
|---|---|---|---|
| `userdata` (`@Primary`) | **d8aforce** | `jdbcUserData` **and the JPA entity manager** | `Application.java:134`, `:277-286` |
| `serverdata` | **d8aforce_data** | `jdbcServerData` only, via `DBService.getJdbcServer()` | `Application.java:139` |

Reference data is therefore split across both databases, by access path rather than by purpose:

| Regulator | Dev database | How it is read | Used by |
|---|---|---|---|
| CFA | `d8aforce_data` | JDBC `getJdbcServer()` | classification |
| CRD | `d8aforce_data` | JDBC `getJdbcServer()` | classification |
| CFP | `d8aforce_data` | JDBC `getJdbcServer()` | classification |
| SEC | `d8aforce_data` | JDBC `getJdbcServer()` | classification |
| SEC | `d8aforce` | JPA `SecInvestorRepository` | investor detail lookup |
| NFA | `d8aforce_data` | JDBC `getJdbcServer()` | classification |
| NFA | `d8aforce` | JPA `NfaSearchFirmRepository` | investor detail lookup |
| CSA | `d8aforce` | JPA `CsaRepository` | **classification** |
| ADV | `d8aforce` | not referenced anywhere in the backend | — |

### Two things this layout implies

**SEC and NFA are reachable in both databases through different code paths.** Classification reads
them from `d8aforce_data` over JDBC; `InvestorService.findSecInvestor` / `findNfaInvestor` read the
same logical tables from `d8aforce` over JPA to render investor details. If the two copies drift,
a record can be classified from one dataset and displayed from another. Refresh both, or treat a
mismatch between a classification result and the detail view as expected rather than a bug.

**CSA is the exception among regulators** — its reference data lives in `d8aforce` (the application
database) and is read by the classification step itself through JPA. It is not part of the JDBC
reference set, so a `d8aforce_data` refresh does not touch it.

**ADV tables are dead weight from the backend's perspective.** `adv_investors`, `adv_companies`,
`adv_connector`, `adv_company_addresses` and `adv_addresses_connector` are produced by the parser
but referenced by no code in this repository. Confirm with whoever owns the parser before assuming
they can be dropped.

### d8aforce_data (serverdata) — parser-owned. Never edit by hand.

Read-only from the application; the parser truncates and rewrites these on each re-parse, so
anything inserted manually is lost at the next run. Flyway migrations here are DDL only.

| Table | Read by |
|---|---|
| `cfa_investors` | CFA Search |
| `crd_investors`, `crd_connector`, `crd_companies`, `crd_company_addresses`, `crd_investor_address_connector` | CRD Search |
| `sec_investors`, `sec_connector`, `sec_companies`, `sec_company_addresses`, `sec_addresses_connector` | SEC Search |
| `cfp_investor`, `cfp_company`, `cfp_address_connector`, `cfp_address` | CFP Search |
| `nfa_search_firms` | NFA Search |
| `occupation_terms` | Occupation Verification |

### d8aforce (userdata) — application-owned. Safe to modify through the UI.

All JPA entities, plus reference tables that are easy to mistake for parser output:

| Table | Purpose |
|---|---|
| `csa_investors` | CSA Search reference data — **app database, read during classification** |
| `sec_investors`, `nfa_search_firms` | Second copies, read only for investor detail lookup |
| `email_suffix` | Email Search domain/prefix types. **App-owned** — has a `manually_added` flag and survives re-parsing. |
| `name_search` | Check Search Name dictionary. **App-owned**, which is why it is absent from the parser export. |
| `zip_code` | Distance cache, filled from the address API on demand |
| `users`, `invites`, `password_resets`, `subscribers` | Accounts |
| `investors`, `unprocessed_investors`, `batches`, `classifications`, `search_results`, `search` | Batch processing and results |
| `configuration` | CS STEPS thresholds and enabled flags |
| `audit_logs` | Audit trail |
| `adv_*` | Parser output, unreferenced by the backend |

### Practical rules

- **Never hand-edit anything in `d8aforce_data`.** It is regenerated wholesale.
- Test investors belong in `d8aforce` (uploaded as a batch), never in the reference database.
- Freezing test *inputs* in `d8aforce` does not stabilise results, because the reference data they
  are matched against still moves. Deterministic algorithm tests belong in the H2 suite
  (`src/test/resources/data-server.sql`), not against a live database.
- `email_suffix`, `name_search` and `csa_investors` being app-owned means seeding them for testing
  is legitimate and survives a re-parse.
- `entityManagerFactory` sets `generateDdl(true)` against `d8aforce`, so Hibernate may alter that
  schema at startup alongside Flyway. Worth knowing before debugging schema drift there.
