# Collected Tor and Direct-Traffic Flow Data

This dataset contains 6,709 flow records: direct browsing (1,803), direct file transfer (1,705), Tor browsing (1,685), and Tor file transfer (1,516). Labels indicate acquisition conditions, not verified per-flow Tor transport. Direct-file-transfer records have loopback endpoints and are retained for collection audits only.

## Files

- `data/`: four flow tables.
- `data_dictionary.csv`: column definitions and the 12 predictors.
- `validation_report.csv`: feature and grouping preservation checks.

ISCXTor2016 is not included. Obtain it from the [official provider](https://www.unb.ca/cic/datasets/tor.html).

## Privacy

IP addresses and ports use consistent random pseudonyms. Absolute timestamps, calendar dates, and the unused original label are removed. No target lists, packet captures, or identifier mappings are distributed. Retained flow statistics and relationships may still permit linkage.

## Analysis

Use only columns marked `predictor` as model inputs. Select the two browsing conditions for classification, with Tor browsing positive. Select `in_shared_date_browsing == 1` for the overlapping shared-date subset.

Within each population, join records sharing either an undirected protocol-and-endpoint key or an identical full predictor vector, then compute connected components. Counts are 5,792 for all records, 3,258 for browsing, and 2,950 for shared-date browsing.

Read CSVs with `float_precision="round_trip"`. Empty numeric entries are missing values. Fit imputation and scaling on training data only.
