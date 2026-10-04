# How to take off a duct job

The step-by-step guide, also live in [English](https://ductforge.debugswift.com/guide), [বাংলা](https://ductforge.debugswift.com/guide/bn) and [हिन्दी](https://ductforge.debugswift.com/guide/hi).

Nothing is stored anywhere but your own device, so you can experiment freely. There's nothing to break.

## First, the one decision that matters

The same duct is a different quantity depending on who's asking. Pick the wrong one and every figure below it is wrong in a way that looks completely reasonable.

- **Billing:** mean perimeter × centreline length (BOQ / IS 655 / DW 144 practice). Use it when you're claiming against a client, consultant or quantity surveyor.
- **Shop:** the true unfolded blank a fabricator cuts. Use it when you're buying sheet or setting a shop to work. Never claim it as a billing quantity.

The formulas behind both are in [standards.md](standards.md).

## The workflow

1. **Set the standard, units and material.** Both switches are in the top bar and apply to the whole takeoff. Switch units whenever you like: geometry is stored in millimetres, so nothing is lost. Material (galvanised, stainless, aluminium) changes the weight, never the area.
2. **Pick the fitting.** Plain run: Straight. Changes size: Transition. Turns: Elbow. Steps sideways: Offset. Branches: Collar or Y-piece. Off an air-handling unit into spiral: Square to round. A plate, blank or end cap: pick it from Flat pieces by its shape.
3. **Type the dimensions.** Each field carries the symbol used in the formula, and the working is shown under the result with your numbers in it. Watch `R`: on a rectangular elbow it's the *inside* radius; on a round elbow it's the centreline radius (usually 1.5 × the diameter).
4. **Check the drawing.** Blueprint shows every dimension in the formula. Flat pattern shows the blanks: solid lines cut, dashed lines fold. Isometric shows the object, the fastest way to spot an offset you meant to be a transition.
5. **Set quantity and waste allowance.** 0% for a net BOQ claim, 8% for factory-run straight duct, 12% for standard flanged work, 15 to 20% for complex fittings and heavy gauge. Gauge is picked from the largest dimension; override it wherever your specification differs.
6. **Add it to the takeoff.** Nothing is scheduled until you press Add. Every line can be edited, duplicated or removed later. Duplicate, then change the length, to take off a run of similar fittings.
7. **Zones, insulation, flanges and hangers.** A zone is whatever you bill by (AHU-1, Level 3, Kitchen); lines with the same zone total together. Insulation, flanges and hangers are off until you switch them on, because a quantity nobody asked for is a quantity nobody checked.
8. **Extras.** Dampers, grilles, diffusers, access doors, flexible duct, and your own lines like labour or transport. Extras are counted, not calculated, and never added to the duct's area or weight.
9. **Read the totals and export.** Net area, waste, gross area and weight, then material by gauge with an estimated sheet count for each. Add your rate per kg or per m² to price the job. Export gives you a PDF quantity sheet (every part switchable, previewed live), CSVs with every input beside every result, and a project file you can reopen or hand on.

## Worth knowing

- **Gauge is chosen by size alone.** Real SMACNA selection also depends on pressure class and reinforcement spacing.
- **Round duct is graded on the rectangular table,** so it comes out over-specified.
- **Sheet counts are an estimate:** gross area over one sheet, rounded up, per gauge.
- **Everything lives on your device.** Clearing browser data clears your takeoffs. If a job matters, Save it to a file.
