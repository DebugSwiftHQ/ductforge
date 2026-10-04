# Standards, formulas and constants

Everything DuctForge calculates, written out, including what it simplifies. The live version is at [ductforge.debugswift.com/standards](https://ductforge.debugswift.com/standards), generated from the same code that computes your takeoff.

**In one line:** surface area comes from the fitting's own dimensions. Gross area is that plus the allowance you set. Weight is gross area times the sheet density printed beside it. Multiply the two numbers on screen and you always get the third.

## One duct, two legitimate quantities

A quantity surveyor and a sheet-metal shop measure the same fitting differently, and both are right. DuctForge keeps them apart and states which one produced every figure.

| | Commercial billing | Shop fabrication |
|---|---|---|
| **What it measures** | Mean perimeter × centreline length (BOQ / IS 655 / DW 144 practice) | The true unfolded blank a fabricator cuts |
| **Includes** | Nominal measurement only | Slant hypotenuses on transitions, heel arc expansion on bends, wrapper triangulation |
| **Use it for** | Invoice claims checked by MEP consultants, clients and quantity surveyors | Buying sheet and setting a shop to work |

They don't always differ, and where they agree it's worth knowing why:

- A **straight duct** has no slant and no arc, so both give the same area.
- An **elbow** agrees too. Its `2·cheek + heel + throat` development simplifies exactly to mean perimeter × centreline arc. That's Pappus's theorem, not a coincidence.
- An **offset** goes the other way: its shop blank is *smaller* than its billed area, because the side cheeks are parallelograms, and shearing a parallelogram adds no area.

## Every fitting, both standards

`W` and `H` are the duct's width and height, `L` its length, `R` the inside (throat) radius, `θ` the included angle, `O` an offset's lateral step and `F` a collar's flange lip. On flat pieces, `D` and `d` are an outside and a hole diameter, `w` and `h` a frame's opening, and `B` and `T` a base and a top edge.

### Rectangular

| Fitting | Commercial billing | Shop fabrication |
|---|---|---|
| Straight duct | `A = 2(W + H) × L` | `A = 2(W + H) × L` |
| Transition | `A = (W₁ + H₁ + W₂ + H₂) × L` | `A = (W₁ + W₂)·√(L² + ((H₁−H₂)/2)²) + (H₁ + H₂)·√(L² + ((W₁−W₂)/2)²)` |
| Elbow | `A = 2(W + H) × [θπ/180 × (R + W/2)]` | `A = 2·A_cheek + A_heel + A_throat`, where `A_cheek = θπ/360·[(R+W)² − R²]`, `A_heel = θπ/180·(R+W)·H`, `A_throat = θπ/180·R·H` |
| Offset | `A = 2(W + H) × √(L² + O²)` | `A = 2(L × H) + 2(W × √(L² + O²))` |
| Collar | `A = 2(W + H) × (L + F)` | `A = 2(W + H)·L + 2(W + H)·F + 4F²` |
| Y-piece | `A = A_B1 + A_B2`, where `A_Bn = (W₁/2 + H + Wₙ + H) × θπ/180·(R + Wₙ/2)` | `A = Σ branches [2·A_cheek + A_heel + A_throat]`, each branch on its own width `Wₙ` |

### Round

| Fitting | Commercial billing | Shop fabrication |
|---|---|---|
| Round duct | `A = πD × L` | `A = πD × L` |
| Round elbow | `A = πD × [θπ/180 × R]` | `A = πD × [θπ/180 × R]` |
| Round reducer | `A = π(D₁ + D₂)/2 × L` | `A = π(D₁ + D₂)/2 × √(L² + ((D₁−D₂)/2)²)` |
| Square to round | `A = [2(W + H) + πD]/2 × L` | `A = W·√(L² + ((H−D)/2)²) + H·√(L² + ((W−D)/2)²) + 4 × ½∫₀^{π/2} r·√(L² + (r − (W/2)cos φ − (H/2)sin φ)²) dφ`, with `r = D/2` |

### Flat pieces

A flat piece is one face with nothing to unfold, so both standards give the same area. It isn't a length of duct, so it's never counted for flanges, corner pieces or hangers.

| Piece | Area |
|---|---|
| Rectangular plate | `A = W × H` |
| Round plate | `A = πD²/4` |
| Ring | `A = π(D² − d²)/4` |
| Plate with round hole | `A = W × H − πd²/4` |
| Rectangular frame | `A = W × H − w × h` |
| Flat-oval plate | `A = (W − H) × H + πH²/4` |
| Triangular plate | `A = B × H / 2` |
| Trapezoid plate | `A = (T + B)/2 × H` |

## What each one assumes

- **Transition:** concentric, with both openings on one centreline. An eccentric (flat-on-one-side) reducer has a larger slant on the offset face and isn't modelled.
- **Elbow:** `R` is the inside (throat) radius, so the centreline radius the billing formula uses is `R + W/2`. Both standards agree, because a swept constant section develops exactly to its mean perimeter (Pappus). An elbow bills what it cuts.
- **Offset:** the only fitting where the shop blank comes out smaller than the billing area. Both figures are correct; they answer different questions.
- **Collar:** the shop blank is the billing area plus the four corner squares at the flange, the material the billing standard treats as scrap.
- **Y-piece:** *our stated interpretation, not a published formula.* The source specification gives the shop area only as "sectors + heels + throats", so each branch is developed as an elbow on its own width. The crotch (splitter) plate is **not** included; add it as a separate line if your shop cuts one. The two standards cross over at `Wₙ = W₁/2`: a branch narrower than half the main duct bills for more than it cuts.
- **Round duct:** a cylinder unrolls with no distortion, so both standards agree. Spiral-wound duct uses a continuous strip: the area is the same, the cutting isn't.
- **Round elbow:** both standards agree, by Pappus's theorem. The gore count changes the blanks and the cutting waste, never the surface area.
- **Round reducer:** the blank is an annular sector, so the shop area uses the *slant* height, not the length. Concentric only.
- **Square to round:** four flat triangles and four conical corner patches, the exact surface of the standard construction. The corner term has no closed form, so it's integrated numerically. Concentric only.
- **Flat-oval plate:** the shorter of `W` and `H` is the diameter of the round ends.
- **Triangle and trapezoid:** the area depends only on the base, top and height, wherever the apex or top edge sits.

## Sheet gauge by largest dimension

The common size-only shortcut from the SMACNA duct construction standards. The metric and imperial bands are two published tables, not conversions of each other (12 inches is 304.8 mm), so a job is graded on the table matching its own units.

| Gauge | Thickness | Largest dimension (metric) | Largest dimension (imperial) | kg/m² | lb/ft² |
|---|---|---|---|---|---|
| 26 ga | 0.55 mm | up to 300 mm | up to 12″ | 4.32 | 0.885 |
| 24 ga | 0.70 mm | 301 to 750 mm | 13″ to 30″ | 5.50 | 1.126 |
| 22 ga | 0.85 mm | 751 to 1000 mm | 31″ to 40″ | 6.67 | 1.366 |
| 20 ga | 1.00 mm | 1001 to 1500 mm | 41″ to 60″ | 7.85 | 1.608 |
| 18 ga | 1.20 mm | 1501 to 2100 mm | 61″ to 84″ | 9.42 | 1.929 |
| 16 ga | 1.60 mm | over 2100 mm | over 84″ | 12.56 | 2.572 |

**This is a simplification, and it matters.** Real gauge selection also depends on the duct's pressure class and reinforcement spacing. Treat the table as a starting point, check it against the project specification, and override the gauge by hand wherever the spec differs. The override carries through to the weight, the sheet count and the export.

Densities are derived, not transcribed: thickness × 7850 kg/m³, which reproduces the published table exactly. That's bare metal, with no coating, stiffeners, flange steel, gaskets or fixings.

**Round duct** is graded on the rectangular table, because that's the table DuctForge has. SMACNA publishes a separate, generally lighter table for round and spiral duct (a cylinder is stiffer than a flat panel), so round comes out over-specified.

## Material

A gauge is a thickness, so the band table survives a change of material. Only the density moves, and with it the weight.

| Material | Density | Note |
|---|---|---|
| Galvanised steel | 7850 kg/m³ | Bare steel. The zinc coating adds roughly 1% and isn't counted. |
| Stainless steel | 8000 kg/m³ | Austenitic (304 / 316). Ferritic grades run nearer 7700 kg/m³. |
| Aluminium | 2700 kg/m³ | The gauge table is a steel standard. Aluminium duct is normally specified a gauge or two heavier for the same duty. |

## Insulation, flanges and hangers

Each is derived from the geometry you already typed, and each is off until you switch it on.

- **Insulation:** the billing formula re-run with every cross-section dimension grown by twice the thickness. Lagging a 600 × 400 duct with 25 mm measures it as 650 × 450. The centreline never moves: a rectangular elbow's throat radius shrinks by the thickness while its width grows by twice it.
- **Flanges:** a flange at each end of every piece, and a straight run is as many pieces as the supplied length divides into. A 6 m run of 1.2 m duct is five pieces, so ten ends. Corner pieces are four per rectangular end; a round flange has none.
- **Hangers:** one support per piece, plus one for each further full spacing of centreline run. A rule of thumb, not a structural calculation.

Rates work the same way in reverse: your own figure per kg or per m², applied to these quantities. DuctForge has no prices of its own.

## Waste allowance presets

The allowance is your decision, not a measurement. Any line can carry its own figure, and every export states which was used.

| Allowance | Where it applies |
|---|---|
| 0%: net BOQ | Pure theoretical area, for direct subcontractor invoicing |
| 8%: slip and drive | Factory-run straight duct in light gauge, minimal seam scrap |
| 12%: industry standard | SMACNA / TDF / TDC transverse flange roll-forming: a 35 mm flange lip per side plus the longitudinal Pittsburgh seam |
| 15%: heavy fittings | Complex multi-branch fittings and angle-iron companion flanges |
| 20%: high wastage | Heavy gauge sheet, awkward nesting, high offcut loss |

## Why the sheet count is only an estimate

Gross area divided by one commercial sheet (2.88 m² at 1200 × 2400 mm, or 32 ft² at 4 × 8 ft), rounded up, and counted separately for each gauge.

- **Per gauge, never in total.** 22 ga can't be cut from a 24 ga sheet, so a combined count would be a number you couldn't take to a merchant.
- **It ignores nesting.** A real shop reuses offcuts, and some blanks don't tile. The true figure moves in both directions.
- **Seam laps are in the allowance, not the drawing.** The flat patterns show the developed blank only; drawing seams as well would count them twice.
