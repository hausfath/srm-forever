# SRM Forever?

An interactive, deliberately simple model of a question raised by colleagues: **could it make economic sense to decarbonize slowly while holding global temperature at 1.5°C with stratospheric aerosol injection (SAI) for as long as it takes, rather than mitigating rapidly and drawing temperatures back down with carbon removal?**

**Live tool:** https://hausfath.github.io/srm-forever/

Both scenarios reach zero emissions and end at 1.5°C; they differ in how fast, and in how long the commitment runs. Every number on the page recomputes from the inputs.

## The two scenarios

| | SRM scenario | Mitigation + CDR scenario |
|---|---|---|
| Gross emissions | 40 GtCO₂/yr through 2030, linear to zero in 2200 (~3,600 GtCO₂ cumulative) | 40 GtCO₂/yr through 2030, linear to zero in 2070 (~1,000 GtCO₂ cumulative) |
| Temperature management | SAI holds 1.5°C; deployment ends when slow post-emission cooling (the ZEC drift) returns the underlying climate to the target on its own (~year 18,300 at central TCRE, 11,800–24,800 across the AR6 likely range) | CDR (default 2 GtCO₂/yr from 2070) until temperature first returns to 1.5°C (~2525 at defaults), then permanent net zero |

## Model structure

- Annual timestep from 2025 (warming set to 1.5°C above 1850–1900). The horizon is endogenous: the simulation runs until the highest-TCRE variant's SRM requirement ends, capped at 100,000 years.
- Temperature: T(t) = 1.5°C + TCRE × cumulative net CO₂ / 1000 + ZEC drift × (t − 2025)/1000, floored at preindustrial.
- SRM cost: (cooling/0.1°C)^k × $B-per-0.1°C, default anchor $1.8B (Smith 2020) and exponent k = 1.3 (Niemeier & Timmreck 2015 forcing saturation over this scenario's 1–2.3°C peak-cooling range).
- Abatement is charged only while a path's gross emissions are still falling ("transition only"); cost accounting is selectable (total vs. constant 40 Gt baseline, or incremental vs. the SRM path) and flows through every output including the breakeven discount rate.
- NPV with a constant exponential discount rate (default 1%); the breakeven rate is found by bisection.

Full methods, parameter tooltips, a data table, and caveats are documented in the page itself.

## Key sources (verified against primary texts)

- **TCRE:** IPCC AR6 WG1 [SPM D.1.1](https://www.ipcc.ch/report/ar6/wg1/downloads/report/IPCC_AR6_WGI_SPM.pdf) — best estimate 0.45°C per 1,000 GtCO₂, likely range 0.27–0.63.
- **ZEC:** AR6 WG1 [Ch. 4 §4.7.1.1](https://www.ipcc.ch/report/ar6/wg1/downloads/report/IPCC_AR6_WGI_Chapter04.pdf) — ZEC50 mean −0.079°C, 5–95% −0.34 to +0.28°C. The −0.1°C/1,000 yr drift default is this tool's own anchor for multi-millennial cooling; AR6 does not assess one.
- **SAI deployment cost:** [Smith (2020), *Environ. Res. Lett.* 15, 114004](https://doi.org/10.1088/1748-9326/aba7e7) — ~$18B/yr per °C (2020 USD); [Smith & Wagner (2018)](https://doi.org/10.1088/1748-9326/aae98d).
- **Forcing saturation:** [Niemeier & Timmreck (2015), *Atmos. Chem. Phys.* 15, 9129](https://acp.copernicus.org/articles/15/9129/2015/), Eq. (1); [Kleinschmitt et al. (2018), *Atmos. Chem. Phys.* 18, 2769](https://acp.copernicus.org/articles/18/2769/2018/), who find a ~−1.9 W/m² ceiling for equatorial injection — a structural limit no cost exponent captures.

## Headline behavior (defaults)

At the default settings (total accounting, 1%/yr discounting, $30/t mitigation, $100/t CDR at 2 GtCO₂/yr, SRM $1.8B per 0.1°C with exponent 1.3), **mitigation + CDR is cheaper** (~$30T vs. ~$38T NPV), with a breakeven discount rate of ~1.7%. Under incremental accounting the breakeven drops to ~0.06%. The verdict turns almost entirely on the discount rate, the cost accounting, and the ZEC extrapolation — the tool is built to make those dependencies explicit rather than to hide them.

## Major caveats

This is a toy model for structuring a discussion, not a projection. Damages are not priced on either side; SRM termination risk, ocean acidification, regional climate effects, and governance costs are not priced; CDR and mitigation prices are flat forever; the SRM end date rests entirely on extrapolating a per-millennium ZEC drift that AR6 does not assess. See the caveats section in the page.

## Repository

The tool is a single self-contained `index.html` (no build step, no dependencies beyond Google Fonts). To reproduce or modify, edit the file and open it in a browser.

## License

Code is MIT licensed (see [LICENSE](LICENSE)). IPCC AR6 figures and the cited papers remain under their publishers' terms.
