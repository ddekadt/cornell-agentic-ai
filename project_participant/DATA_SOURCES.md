# Data sources

All original data lives under `data/raw/` and is **never modified**. Everything here was retrieved on 2026-09-09 and is free to redistribute — US federal government works are in the public domain.

The unit of analysis throughout is the **census tract**. There are **2,327 tracts** covering the five boroughs of New York City.

## Income and other attributes

- **Folder:** `data/raw/acs/`
- **Source:** US Census Bureau, American Community Survey, ACS 2020-2024 5-year, table-based Summary File.
- **Retrieved from:** <https://www2.census.gov/programs-surveys/acs/summary_file/2024/table-based-SF/>
- **Documentation:** <https://www.census.gov/programs-surveys/acs/data/summary-file.html>

Each file is one ACS table, filtered from the national release to NYC tracts and joined to a readable tract name and borough.

| File | Table | Contents | Columns |
|---|---|---|---|
| `acs/b01003.csv` | B01003 | Total population | 2 |
| `acs/b01001.csv` | B01001 | Sex by age | 98 |
| `acs/b03002.csv` | B03002 | Race and Hispanic or Latino origin | 42 |
| `acs/b05002.csv` | B05002 | Place of birth by nativity and citizenship | 54 |
| `acs/b11001.csv` | B11001 | Household type | 18 |
| `acs/b15003.csv` | B15003 | Educational attainment (25+) | 50 |
| `acs/b17001.csv` | B17001 | Poverty status in the past 12 months | 118 |
| `acs/b19013.csv` | B19013 | Median household income | 2 |
| `acs/b25003.csv` | B25003 | Tenure (owner/renter) | 6 |
| `acs/b25077.csv` | B25077 | Median house value (owner-occupied) | 2 |
| `acs/b27001.csv` | B27001 | Health insurance coverage by sex by age | 114 |
| `acs/b08301.csv` | B08301 | Means of transportation to work | 42 |

Columns ending `_E###` are **estimates**; those ending `_M###` are **margins of error**. ACS is a survey, not a census — the margins matter, especially at tract level.

**Missing values are coded `-666666666`** (and `-222222222` for margins). These are not zeros or negative incomes. They mean the estimate was suppressed or could not be computed — typically parks, cemeteries, airports and other tracts with very few households. Filter them out before doing arithmetic.

## Tract boundaries

- **File:** `data/raw/nyc_tracts_2024.geojson`
- **Source:** US Census Bureau, TIGERweb, Census Tracts layer.
- **Retrieved from:** <https://tigerweb.geo.census.gov/arcgis/rest/services/TIGERweb/Tracts_Blocks/MapServer/0>
- Already in WGS84 (EPSG:4326) and clipped to the five boroughs. Join to the ACS tables on `GEOID`.

## Joining the pieces

The ACS files carry a `geoid` like `1400000US36061000100`. The boundary file's `GEOID` is the last part only, `36061000100`. Strip the prefix before joining:

```r
income$GEOID <- sub("^1400000US", "", income$geoid)
```

## Checksums

If you want to verify the source files are what we say they are:

| Table | Source file bytes | SHA-256 of source |
|---|---|---|
| B01003 | 18,313,708 | `38d1a992bb058d184009b10b9b349872…` |
| B01001 | 200,356,282 | `1637b18a96881b81e050df1cd3d5ac38…` |
| B03002 | 83,256,772 | `ef1a9310905393bf477820de8edb2935…` |
| B05002 | 57,767,821 | `7c97161f6a299ba213b54acad4fc869b…` |
| B11001 | 45,827,971 | `77200c3d9c0d99773bc7f78208bc96f2…` |
| B15003 | 92,292,840 | `d0c8609e958022459215c8a31d7452ef…` |
| B17001 | 118,607,125 | `707adda8aaff136382f4fe0858617d09…` |
| B19013 | 17,917,916 | `b25a176b0e6c339b6f3a2a0d3d8446bf…` |
| B25003 | 26,901,770 | `68e963e1ed60fcf6b0658579cefc6498…` |
| B25077 | 18,496,426 | `89eb2153764a2330b23959d8bbc29b3a…` |
| B27001 | 119,572,124 | `af9b1cad8178ebc85fa96a32b615a3f7…` |
| B08301 | 88,492,616 | `552b24c135b6e7c566910914a861cda6…` |

## Want something else?

Any other ACS table can be added the same way — browse them at <https://data.census.gov> and fetch from the Summary File directory above. The full list of table IDs is at <https://www.census.gov/programs-surveys/acs/technical-documentation/table-shells.html>.
