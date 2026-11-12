# France Public Contract Winners by SIREN (DECP)

[![Apify Actor](https://img.shields.io/badge/Apify-Actor-1f6feb)](https://apify.com/phonic_lily/france-public-contract-winners) ![Licence](https://img.shields.io/badge/licence-Licence_Ouverte_2.0-blue) ![Records](https://img.shields.io/badge/records-39%2C490-green)

French public contract winners aggregated by supplier SIREN: contracts, declared total EUR, buyers, CPV codes, region, years. Embedded data, pay per row.

## What you get
- **39,490 records**, each carrying its own `license` and `attribution` fields, ready to republish with the required credit.
- A **100-record free sample** in this repository: [`sample.jsonl`](sample.jsonl) and [`sample.csv`](sample.csv) (opens as a table on GitHub).
- The **full dataset** as a filterable API (JSON, CSV, Excel), no scraping, no login: [France Public Contract Winners by SIREN (DECP) on Apify](https://apify.com/phonic_lily/france-public-contract-winners).

## One record
```json
{
  "supplier_siren": "005620190",
  "supplier_name": "L'OISEAU BLEU",
  "supplier_size": "ETI",
  "supplier_city": "Abbeville",
  "supplier_department": "Somme",
  "supplier_region": "Hauts-de-France",
  "contracts_count": 15,
  "contracts_with_amount_count": 12,
  "contracts_amount_excluded_count": 0,
  "total_declared_amount_eur": 6427545.0,
  "first_notification_date": "2020-09-14",
  "last_notification_date": "2025-07-02"
}
```

## Quick start
Python:
```python
from apify_client import ApifyClient
client = ApifyClient('<YOUR_APIFY_TOKEN>')
run = client.actor('phonic_lily/france-public-contract-winners').call(run_input={'maxResults': 10})
for item in client.dataset(run['defaultDatasetId']).iterate_items():
    print(item)
```
Or from the command line:
```bash
curl -X POST 'https://api.apify.com/v2/acts/phonic_lily~france-public-contract-winners/run-sync-get-dataset-items?token=<YOUR_APIFY_TOKEN>' \
  -H 'Content-Type: application/json' -d '{"maxResults": 10}'
```
Pricing is pay-per-record on Apify (see the Actor page); the sample here is free.

## Fields
| Field | Description |
|---|---|
| `supplier_siren` | Supplier SIREN (9 digits). |
| `supplier_name` | Most frequent legal name of the supplier. |
| `supplier_size` | PME / ETI / GE, null if unknown. |
| `supplier_city` | City of the supplier on its latest contract. |
| `supplier_department` | Department name of the supplier. |
| `supplier_region` | Region derived from the department, null for overseas collectivities. |
| `contracts_count` | Number of distinct contracts. |
| `contracts_with_amount_count` | Contracts with a usable declared amount (counted in the total). |
| `contracts_amount_excluded_count` | Contracts whose amount was left out because flagged suspect or aberrant. |
| `total_declared_amount_eur` | Sum of usable declared amounts in EUR, null if none, never 0. |
| `first_notification_date` | Earliest notification date (ISO). |
| `last_notification_date` | Latest notification date (ISO). |
| `distinct_buyers_count` | Number of distinct buyers (SIRET). |
| `top_buyers` | Up to 5 buyers: buyer_siret, buyer_name, contracts. |
| `top_cpv_codes` | Up to 5 CPV codes: cpv_code, contracts. |
| `top_cpv_codes_list` | Space-separated top CPV codes (used by cpvPrefix). |
| `active_years` | Notification years with at least one contract. |

## Data, licence and attribution
Built from the DECP consolidated dataset (data.gouv.fr, Licence Ouverte 2.0), as already embedded in the four Actors france-public-contracts-decp-2000-2020, -2021-2022, -2023-2024 and -2025-2026 (current data only, notification dates up to 2026-07; suppliers are legal entities only, verified against INSEE SIRENE). One row per supplier SIREN, all years combined. Method: contracts_count counts distinct contract uids (a contract with several co-contractors counts once for each). The declared contract amount (amount_eur) is credited in full to every co-contractor, it is not split between them. total_declared_amount_eur is the sum of the strictly positive declared amounts of the supplier's contracts; contracts whose amount the source flags as suspect or aberrant (amount_flag) are excluded from the sum and counted in contracts_amount_excluded_count; amounts declared as 0 are ignored; the total is null when no usable amount exists, never 0. Supplier name, size, city and department are those of the supplier's most recently notified contract; supplier_region is derived from the department (null for overseas collectivities without a region such as Saint-Martin). top_buyers and top_cpv_codes list the 5 most frequent buyers and CPV codes by number of distinct contracts (ties broken by identifier). Rows whose legal name starts with a civility title (Monsieur, Madame, Dr...) are removed as probable individuals. Aggregates describe notified contracts as published in DECP, which is known to be incomplete and sometimes inaccurate: they are not a measure of a company's revenue.

**Licence:** Licence Ouverte 2.0 (Etalab)

**Attribution:** Source: data.gouv.fr, Donnees essentielles de la commande publique (DECP) consolidees, Licence Ouverte 2.0 (Etalab); supplier verification with INSEE SIRENE. Aggregated by SIREN from the france-public-contracts-decp-* Actors.

Snapshot date: 2026-07. Empty values are `null`, never 0.

## Cite this dataset
GitHub's *Cite this repository* button reads [`CITATION.cff`](CITATION.cff).

## Feedback
Found an error or want a field added? Open an issue in this repository.
