# 3D Printer Calibration Workflow

## Purpose

This document defines the recommended order for configuring and calibrating a 3D printer.

Calibration should be performed in sequence because each adjustment affects the next.  
Do not tune advanced settings until mechanical alignment, extrusion, and first-layer performance are correct.

---

# Calibration Order Overview

1. Mechanical Inspection
2. Bed Leveling / Z-Axis Calibration
3. Extruder Calibration
4. First Layer Calibration
5. Temperature Calibration
6. Retraction Calibration
7. Flow Calibration
8. Pressure Advance / Linear Advance
9. Speed Optimization
10. Dimensional Accuracy
11. Final Profile Backup

---

# 1. Mechanical Inspection

Before changing software settings, verify printer hardware.

## Check:

- [ ] Frame is square
- [ ] Gantry is level
- [ ] Belts are tensioned
- [ ] V-wheels/linear rails move smoothly
- [ ] Lead screws are clean and aligned
- [ ] No excessive play in axes
- [ ] No loose hotend components
- [ ] No nozzle damage

---

# 2. Z-Axis / Bed Calibration

## Goal

Establish the correct nozzle-to-bed distance.

Incorrect Z-offset causes:

### Too High

Symptoms:

- Lines do not stick
- Gaps between extrusion lines
- Corners lift
- First layer looks rounded

Adjustment:

```
Decrease Z-offset
(move nozzle closer to bed)
```

---

### Too Low

Symptoms:

- Plastic is squished excessively
- Rough first layer
- Extrusion becomes inconsistent
- Nozzle drags through print

Adjustment:

```
Increase Z-offset
(move nozzle away from bed)
```

---

## Tune:

- Bed leveling
- Mesh calibration
- Z-offset
- First-layer height

Recommended starting point:

```
First Layer Height:
0.20 mm

Z Offset:
Calibrate manually

Bed Mesh:
Enable after leveling
```

---

# 3. Extruder Calibration

## Goal

Ensure commanded extrusion matches actual extrusion.

Incorrect extrusion affects:

- Walls
- Infill
- First layer
- Strength
- Dimensional accuracy

---

## Calibrate:

### E-Steps / Rotation Distance

Test:

Command:

```
Extrude 100mm filament
```

Measure actual extrusion.

Adjust:

```
New Value =
(Current Value × Commanded Length)
÷ Actual Length
```

---

# 4. First Layer Calibration

## Goal

Achieve consistent adhesion.

Tune:

- Z-offset
- First layer speed
- First layer extrusion width
- Bed temperature

Recommended starting values:

```
First Layer Speed:
20-30 mm/s

First Layer Width:
120-140%

First Layer Height:
0.20 mm
```

---

# 5. Temperature Calibration

## Goal

Find the best printing temperature.

Perform:

```
Temperature Tower
```

Tune:

- Nozzle temperature
- Bed temperature
- Cooling settings

Evaluate:

- Layer adhesion
- Stringing
- Surface quality
- Overhang performance

---

# 6. Retraction Calibration

## Goal

Reduce stringing during travel moves.

Tune:

- Retraction distance
- Retraction speed
- Travel speed

Too little:

```
Stringing
Blobs
Oozing
```

Too much:

```
Under-extrusion
Heat creep
Grinding filament
```

---

# 7. Flow Calibration

## Goal

Match extrusion volume to slicer calculations.

Tune:

```
Flow Rate / Extrusion Multiplier
```

Symptoms of incorrect flow:

## Too High

- Bulging walls
- Poor dimensions
- Excess material

## Too Low

- Weak walls
- Gaps
- Poor top surfaces

---

# 8. Pressure Advance / Linear Advance

## Goal

Compensate for filament pressure changes during acceleration.

Controls:

- Corner quality
- Sharp edges
- Consistent extrusion

Tune only after:

- Z-offset is correct
- Extruder calibration is complete
- Flow is calibrated

---

## Too Low

Symptoms:

- Rounded corners
- Extra material at corners
- Blobs

---

## Too High

Symptoms:

- Thin corners
- Under-extrusion after acceleration
- Gaps

---

# 9. Speed Optimization

Tune after quality settings are correct.

Adjust:

- Print speed
- Acceleration
- Jerk
- Travel speed

Higher speed requires:

- More extrusion capability
- Better cooling
- More precise pressure advance

---

# 10. Dimensional Accuracy

After extrusion is calibrated:

Print:

```
20mm Calibration Cube
```

Measure:

- X dimension
- Y dimension
- Z dimension

Adjust:

- Steps/mm
- Shrink compensation
- Flow

---

# 11. Final Profile Backup

After calibration:

Backup:

```
Printer Profile
Slicer Profile
Firmware Settings
Material Profiles
```

Record:

```
Printer:
Nozzle:
Material:
Layer Height:
Temperature:
Flow:
Pressure Advance:
Retraction:
Speed:
Acceleration:
```

---

# Calibration Priority

## Highest Impact

1. Z-offset
2. Bed leveling
3. Extruder calibration
4. Temperature
5. Flow

## Advanced Tuning

6. Retraction
7. Pressure Advance
8. Speed
9. Dimensional compensation

---

# Golden Rule

Only change one variable at a time.

Make a test print.

Record the result.

Keep successful profiles.