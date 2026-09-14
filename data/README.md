# Data

## `ff30_daily_returns.csv` (not included)

Daily value-weighted returns of the 30 industry portfolios, 1990-01-02 to
2026-06-30, 9190 trading days, expressed as decimals.

**This file is deliberately not redistributed here.** The Kenneth R. French Data
Library states that its contents are the property of Ken French and Dimensional
Fund Advisors and that use in part or whole requires their permission. The file
is therefore obtained from the source:

```
python3 data/download_ff30.py
```

The script downloads `30_Industry_Portfolios_daily_CSV.zip` from the French Data
Library, extracts the `Average Value Weighted Returns -- Daily` block, restricts
it to the paper's window, converts percent to decimals, and writes the CSV. It
then prints the SHA-256 of what it wrote and compares it against

```
2ba1f734ad41d3a101596b3bc30c358c53da29e13c91f0b9fca8a8e17b0d8af9
```

which is the hash of the vintage retrieved on 14 September 2026, behind every
number reported in the paper. If the hashes match, the reproduction is exact.

If they do not, that is expected over time rather than an error: the French
library is restated periodically as the underlying CRSP data are revised. A
retrieval on 14 September 2026 differed from an earlier one in 32 cells out of
275,700, with a maximum absolute difference of 0.0034, and every published
result was unaffected to the precision reported. The script therefore prints a
notice and exits zero; re-run `reproduce_paper1.sh` to recompute the empirical
results on your own retrieval and compare them against the published values.

The retrieval script has been validated end to end by round trip: the published
CSV was re-encoded into the raw layout of the French daily file (percent returns,
`YYYYMMDD` dates, header block, trailing equal-weighted block), passed through
the script, and the output was byte-for-byte identical to the original, with a
matching SHA-256.

Source: Kenneth R. French Data Library,
<https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html>.
The underlying returns are constructed from CRSP data.

## `noaa_climate_indices.csv` (included)

Monthly values of ten climate oscillation indices (SOI, NAO, PDO, AO, AMO,
NINO34, PNA, WP, EA, EPO), 1951-01 onward, from the U.S. National Oceanic and
Atmospheric Administration. Works of the U.S. federal government are not subject
to domestic copyright protection, so this file is included directly.
