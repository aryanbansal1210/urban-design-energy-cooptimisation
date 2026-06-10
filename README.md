# Urban Design + Energy Co-Optimisation - 3D Digital Twin

**MSc Thesis · Sustainable Energy Futures · Imperial College London (2025-26)**

A platform that designs a new town **and** its clean-energy system *together*, then renders the result as an interactive 3D digital twin you can fly through. This page is a **showcase** of that work.

> **Source code:** kept private by design. This is an active research project I intend to develop into an open-source tool on my own timeline, so the optimisation engine is not published here. Happy to walk through it live (screen-share / interview).

<!-- DEMO: once you upload a screen-recording or GIF, embed it right here, e.g.:
![Flying through the optimised town with the sun-slider casting real-time shadows](demo.gif)
-->


---

## The idea

Master-planning a new town and planning its clean-energy system are normally done separately, one after the other. That misses the biggest lever: **how a district is laid out - building heights, street orientation to the wind, shading, where demand sits, how much roof faces the sun - changes how much energy it needs in the first place.**

This project treats layout and energy as **one coupled optimisation problem**:

1. **Urban-design layer.** A simulated-annealing optimiser places land use, building heights and a connected road network across a **625-cell grid** (a 25 km^2, 5 x 5 km new town for ~100,000 people, Zirakpur, Punjab), under 20+ statutory planning constraints (URDPFI / IPHS norms) and 30+ objectives: solar access, passive cooling, walkability, equity.
2. **Energy layer.** Given a layout, a Pyomo / HiGHS mixed-integer linear program sizes and dispatches rooftop / ground-mount / carport / floating / BIPV solar, Li-ion storage and vehicle-to-grid across **864 representative time-slices**, over a **25-year horizon** (2030 / 2042 / 2055) with CAPEX learning curves and panel degradation.

**Result vs a grid-only baseline:** about **45% lower annual cost** and **57% lower operational CO2**, at roughly 3.84 INR/kWh.

---

## The 3D digital twin (what the demo shows)

The viewer turns the optimiser's output into something you can explore:

- **The optimised town in 3D** - buildings extruded by height tier, colour-coded land use, roads, parks, water, solar farms, carport canopies and energy plant, across around 25 distinct render layers.
- **Real-time sun and shadows** - a time-of-day / date slider moves the sun correctly for the site's latitude, casting geometry-accurate shadows. The *same* shadow physics feeds the energy model's per-cell PV-yield calculation, so the picture and the numbers come from one engine.
- **A live energy cockpit** - tabs for generation, storage, vehicle-to-grid and grid exchange, including an Octopus-Agile-style daily tariff graph, across the 2030 / 2042 / 2055 periods.
- **Click-to-inspect** - click any parcel to read its properties.

Built with **deck.gl / WebGL** (around 7,600 lines of JavaScript), on a custom solar-position and shadow-geometry engine.

---

## Under the hood (engine, kept private)

| Layer | Approach |
|---|---|
| Urban design | Simulated annealing over a 625-cell grid, 20+ hard constraints, 30+ objectives |
| Energy system | Pyomo / HiGHS mixed-integer linear program, 864 time-slices, multi-period (2030/2042/2055) |
| Realism | Physics-based shading, soiling / fog / temperature PV derating, CAPEX learning, degradation |
| Scale | ~24,000 lines (Python + JavaScript), a regression-test suite of ~269 cases |
| Stack | Python · Pyomo · HiGHS · NumPy / pandas · deck.gl / WebGL · GeoJSON |

---

## Demo

Because the engine is private, the best way to see it working is the screen-recording above (no setup needed). If you would like a deeper walkthrough or a live look at the codebase, I am happy to arrange one.

---

*Aryan Bansal - MSc Sustainable Energy Futures, Imperial College London · [LinkedIn](https://www.linkedin.com/in/aryanbansal1210)*
