# Artillery M1 Extras & Macros

This repository contains additional configurations and macros for the Artillery M1 3D printer running Klipper firmware.

## Contents

### [validate_bed_mesh.py](./validate_bed_mesh.py)
A safe Klipper extension that exposes bed mesh interpolation to GCode macros, allowing you to validate the accuracy of your bed mesh and automatically trigger remeshing when deviations are too large.

For more details, see: [README.validate_bed_mesh.py](./README.validate_bed_mesh.py)

### [macros_ellis3d.cfg](./macros_ellis3d.cfg)
A collection of useful Klipper macros from Ellis3D's print tuning guide.

For more details, see: [README.macros_ellis3d.cfg](./README.macros_ellis3d.cfg)

## Installation

1. Copy the desired files to your Klipper extras directory or configuration directory
2. Follow the specific installation instructions in each component's README

## License

See [LICENSE](./LICENSE) file for licensing information.