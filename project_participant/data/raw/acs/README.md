# ACS ACS 2020-2024 5-year — New York City tracts

American Community Survey tables, tract level, five boroughs (2,327 tracts).
Source: US Census Bureau table-based Summary File. See `../../../DATA_SOURCES.md` for provenance and checksums.

| File | Table | Contents | Data columns |
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

Every file shares the same first three columns: `geoid`, `tract_name`, `borough`.

`_E###` columns are estimates, `_M###` are margins of error. **`-666666666` means missing, not zero.**
