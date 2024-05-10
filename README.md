This plugin provides distance metrics on list, arrays and string datatypes in polars.

The docs can be found here: https://ion-elgreco.github.io/polars-distance/

## Examples

```python
import polars as pl
import polars_distance as pld

df = pl.DataFrame({
    "foo":"hello",
    "bar":"hella world"
})

df.select(
    pld.col("foo").dist_str.hamming('bar').alias('dist')
)
┌──────┐
│ dist │
│ ---  │
│ u32  │
╞══════╡
│ 7    │
└──────┘


df.select(
    pld.col('foo').dist_str.levenshtein('bar').alias('dist')
)
┌──────┐
│ dist │
│ ---  │
│ u32  │
╞══════╡
│ 6    │
└──────┘



df = pl.DataFrame(
    {
        "arr": [[1, 2, 10]],
        "arr2": [[2, 5, 9]],
    },
    schema={
        "arr": pl.Array(inner=pl.Float64, width=3),
        "arr2": pl.Array(inner=pl.Float64, width=3),
    },
)
df.select(pld.col('arr').dist_arr.euclidean('arr2').alias('dist'))
shape: (1, 1)
┌──────────┐
│ dist     │
│ ---      │
│ f64      │
╞══════════╡
│ 3.316625 │
└──────────┘
```
