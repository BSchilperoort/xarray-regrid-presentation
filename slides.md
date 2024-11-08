# xarray-regrid

---

## About me
<!-- .slide: style="text-align: left;"> -->
### Bart Schilperoort

Research Software Engineer

Netherlands eScience Center


<hr>

🧑‍💻 [github.com/BSchilperoort](https://github.com/BSchilperoort) 

📧 b.schilperoort@esciencecenter.nl

---

## What does xarray-regrid do?

- regrid *rectilinear* data
- fast and with low memory usage (w/ Dask)
- built on pangeo stack, pure python package

<hr>

```py
import xarray
import xarray_regrid

ds = xr.open_dataset("input_data.nc")
grid = xr.open_dataset("new_grid.nc")

ds.regrid.conservative(grid)
```

---

## Implementation

Lazy regrid methods for rectilinear grids

1. thin wrapper around `xr.interp`:
   - *linear, nearest, cubic*

2. groupby reductions with Flox:
   - *mode, mean, median, min, max, etc.*

3. custom implementation: *conservative*

---

## Conservative

Conservative regridding preserves the integral of the source field.

<hr>

The reduction is applied one dimension at a time:
- (sparse) weights are computed on the fly

- 1 - 10x faster than xESMF
- ETOPO geoid at 21600x43200 grid can be regridded

Note: 1 billion pixels!

---

## Want to know more?
<!-- .slide: style="text-align: left;"> -->

[github.com/xarray-contrib/xarray-regrid](https://github.com/xarray-contrib/xarray-regrid/)

Come talk to me!

---

## Acknowledgements
<!-- .slide: style="text-align: left;"> -->

Contributors:
- Sam Levang (@slevang): improved the conservative routine
- Deepak Cherian (@dcherian): make the flox reductions possible

Funding:
- Netherlands eScience Center grant NLESC.OEC.2022.017