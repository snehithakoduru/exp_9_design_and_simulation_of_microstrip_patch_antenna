# exp_9_design_and_simulation_of_microstrip_patch_antenna
Design and Simulation of a Microstrip Patch Antenna using using Ansys HFSS

# Experiment 9 — Design and Simulation of a Microstrip Patch Antenna Using Ansys HFSS

---

## Aim

To design and simulate a rectangular microstrip patch antenna at a specified resonant frequency using Ansys HFSS, and to study its return loss, VSWR, bandwidth, gain and radiation pattern.

## Software Used

Ansys HFSS (High Frequency Structure Simulator)

---

## Theory

A **microstrip patch antenna** consists of a thin metallic patch on one side of a dielectric substrate, with a ground plane on the other side. It is low profile, lightweight, easy to fabricate and integrate with microwave circuits, making it popular in wireless communication, radar and satellite applications. Its main drawbacks are narrow bandwidth and low gain compared to other antenna types.

### Design Equations

For a rectangular patch operating in the dominant TM₀₁₀ mode, the standard transmission-line model gives:

**1. Width of the patch:**

```
W = (c / 2f_r) × √(2 / (ε_r + 1))
```

**2. Effective dielectric constant:**

```
ε_reff = (ε_r + 1)/2 + (ε_r − 1)/2 × [1 + 12h/W]^(−1/2)
```

**3. Length extension (fringing effect):**

```
ΔL = 0.412h × [(ε_reff + 0.3)(W/h + 0.264)] / [(ε_reff − 0.258)(W/h + 0.8)]
```

**4. Actual length of the patch:**

```
L = c / (2 f_r √ε_reff) − 2ΔL
```

**5. Ground plane dimensions** (typically extended by 6h on each side):

```
L_g = L + 6h
W_g = W + 6h
```

where:

* c = velocity of light
* f_r = resonant (design) frequency
* ε_r = dielectric constant of the substrate
* h = height (thickness) of the substrate

### Feeding Techniques

The patch can be excited using several methods, most commonly:

* **Microstrip line feed** — an edge feed with an inset cut into the patch to match the 50 Ω line impedance.
* **Coaxial (probe) feed** — the inner conductor of a coaxial connector is soldered directly to the patch at a point where the input impedance is 50 Ω.

This experiment uses the **inset microstrip line feed** (or coaxial probe feed, as specified) for excitation.

---

## Design Specifications

| Parameter                          |                 Value |
| ---------------------------------- | --------------------: |
| Resonant frequency \(f_r\)         |               2.4 GHz |
| Dielectric constant \(\epsilon_r\) |                   4.4 |
| Substrate height \(h\)             |                1.6 mm |
| Patch width \(W\)                  |              37.26 mm |
| Patch length \(L\)                 |              28.95 mm |
| Ground plane \(L_g \times W_g\)    |      38.55 × 46.86 mm |
| Feed type                          | Inset microstrip feed |
| Feed line width                    |                3.0 mm |
| Inset depth                        |                  8 mm |


---

## Procedure

1. **Launch Ansys HFSS** and create a new project. Insert an **HFSS Design** with solution type **Driven Terminal** or **Driven Modal**.
2. **Set the model units** to mm.
3. **Draw the substrate:**
   - Create a rectangular box of dimensions L_g × W_g × h and assign the dielectric material (e.g., FR-4, Rogers RT/Duroid) with the required ε_r.
4. **Draw the ground plane:**
   - Create a rectangular sheet of L_g × W_g on the bottom face of the substrate and assign it as a **Perfect E (PEC)** boundary.
5. **Draw the patch:**
   - Create a rectangular sheet of L × W on the top face of the substrate and assign it as **Perfect E (PEC)**.
6. **Design the feed line:**
   - For a microstrip feed, draw a 50 Ω feed line of the calculated width connecting to the patch (with an inset notch if using inset feed), and excite it with a **Lumped Port** at the outer edge.
   - For a coaxial feed, create a via/probe from the ground plane to the patch at the 50 Ω impedance point and excite it with a **Lumped Port** or **Wave Port** at the coaxial cross-section.
7. **Create the air box and radiation boundary:**
   - Draw an air box around the entire structure, at least λ/4 away from the patch on all sides (and above it).
   - Assign the outer faces of the air box as a **Radiation Boundary**.
8. **Set up the analysis:**
   - Add a **Solution Setup** with the solution frequency equal to f_r.
   - Add a **Frequency Sweep** (Interpolating/Fast) covering the band of interest.
9. **Add far-field reports:**
   - Insert a **Far Field Setup** (Infinite Sphere) for the 2-D and 3-D radiation patterns.
10. **Validate and run the simulation** (Validation Check → Analyze All).
11. **Post-process the results:**
    - Plot **S11 (return loss)** vs frequency and note the resonant frequency and −10 dB bandwidth.
    - Plot **VSWR** vs frequency.
    - Plot the **2-D E-plane and H-plane** radiation patterns and the **3-D gain pattern**.
    - Note the **gain**, **directivity** and **radiation efficiency** at resonance.

---

## Observations

| S.No | Frequency (GHz) |  S11 (dB) |     VSWR | Gain (dBi) |
| ---: | --------------: | --------: | -------: | ---------: |
|    1 |            2.20 |      -8.5 |     2.20 |        5.1 |
|    2 |            2.30 |     -13.8 |     1.52 |        5.7 |
|    3 |            2.35 |     -19.6 |     1.23 |        6.0 |
|    4 |        **2.40** | **-25.4** | **1.11** |    **6.2** |
|    5 |            2.45 |     -18.7 |     1.26 |        6.1 |
|    6 |            2.50 |     -12.4 |     1.63 |        5.8 |
|    7 |            2.60 |      -7.5 |     2.48 |        5.3 |



### Graphs


* S11 vs frequency

<img width="960" height="540" alt="S11 vs Frequency (1)" src="https://github.com/user-attachments/assets/788f1ea1-fdf1-4c4d-be60-2e7b72e6f3a4" />


* VSWR vs frequency

<img width="960" height="540" alt="VSWR vs Frequency (1)" src="https://github.com/user-attachments/assets/23264dc4-7098-4921-8d0c-e2265715ff6d" />


* 2-D E-plane and H-plane radiation patterns

<img width="393" height="538" alt="Screenshot 2026-09-23 211851" src="https://github.com/user-attachments/assets/50324206-e22a-4587-a35e-9428042b487f" />



---

## Precautions

1. Ensure the air box / radiation boundary is at least λ/4 away from the patch structure on all sides.
2. Use a fine mesh near the feed point and patch edges for accurate convergence.
3. Verify the substrate material properties (ε_r, loss tangent, thickness) before running the simulation.
4. Check the port impedance and de-embedding settings before reading S11/VSWR values.
5. Validate the geometry (no overlapping or unassigned boundaries) before analysis.

## Result

Resonant Frequency = 2.4 GHz  

Return loss = -25.4 dB

VSWR = 1.11

Gain = 6.2 dBi


## Conclusion

A rectangular microstrip patch antenna was designed and simulated at 2.4 GHz using Ansys HFSS.

