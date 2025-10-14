# Validate Bed Mesh Klipper Extension

A safe Klipper extension that exposes bed mesh interpolation to GCode macros, allowing you to validate the accuracy of your bed mesh and automatically trigger remeshing when deviations are too large.

## Features

- Get interpolated Z values from your bed mesh at specific XY coordinates
- Probe specific points to validate mesh accuracy
- Compare interpolated values with actual measured values
- Automatically trigger remeshing if deviations exceed a threshold
- Check 5 key points on your bed mesh with a single command
- Access mesh data through GCode macros

## Installation

1. Copy `validate_bed_mesh.py` to your Klipper extras directory (usually `/home/pi/klipper/klippy/extras/` or similar)
2. Add the following configuration to your `printer.cfg`:

```ini
[validate_bed_mesh]
# Optional configuration parameters:
# speed: Movement speed during validation (default: 50)
# horizontal_move_z: Z height to move to between points to avoid probe triggering (default: 3)
# deviation: Maximum allowed deviation in mm (default 0.05 mm)
# remesh: Whether to remesh if deviation exceeded (default True)

[validate_bed_mesh]
speed: 50
horizontal_move_z: 3
deviation: 0.05
remesh: True
```

## Usage

### Commands

#### `VALIDATE_BED_MESH_AT`
Get interpolated Z value, probe the actual Z, and calculate the deviation at a specific XY coordinate.

```
VALIDATE_BED_MESH_AT X=100 Y=100
```

Parameters:
- `X`: X coordinate to validate
- `Y`: Y coordinate to validate

The command will respond with the interpolated mesh Z, measured Z, and deviation.

#### `VALIDATE_BED_MESH`
Probes 5 points on the bed mesh (corners and center) and checks if any exceed the maximum deviation threshold. If any point has a deviation exceeding the threshold, it automatically runs `BED_MESH_CALIBRATE`.

```
VALIDATE_BED_MESH [MAX_DEVIATION=0.05] [SAVE_CONFIG=FALSE]
```

Parameters:
- `MAX_DEVIATION`: Maximum allowed deviation before remeshing (default: 0.05mm)
- `SAVE_CONFIG`: Whether to save the config after remeshing (default: FALSE)
- `REMESH`: whether to remesh if deviation exceeded (default from config)
- `MESH_MIN`: <x,y> - override mesh min point (default from bed_mesh config)
- `MESH_MAX`: <x,y> - override mesh max point (default from bed_mesh config)

### Using in Macros

To use the validated mesh data in your macros, you can access these values through the `printer.validate_bed_mesh` object:

- `printer.validate_bed_mesh.last_mesh_z` - Last interpolated Z value from the mesh
- `printer.validate_bed_mesh.last_probed_z` - Last actual probed Z value
- `printer.validate_bed_mesh.last_deviation` - Last calculated deviation


## How It Works

1. The extension calculates an interpolated Z value from your current bed mesh at the specified XY coordinates
2. It moves the toolhead to the validation point (at a safe Z height to avoid triggering the probe)
3. It performs a probe to measure the actual Z position at that point
4. It calculates the deviation between the mesh prediction and the actual measurement
5. Optionally, it can automatically trigger a bed mesh calibration if the deviation is too large

## Requirements

- Klipper firmware with bed_mesh support
- Configured probe (Z probe)
- Bed mesh already calibrated

## Safety Features

- Uses safe Z heights to prevent probe triggering during movement
- Validates probe availability before operation
- Moves to safe positions before probing
- Optional automatic config saving after remeshing

## Use Cases

- Verify bed mesh accuracy before critical prints
- Automatically remesh when bed conditions change
- Integrate mesh validation into print start procedures
- Debug bed leveling issues
- Monitor long-term bed mesh stability