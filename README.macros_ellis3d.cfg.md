# Ellis3D Klipper Macros

This configuration file contains useful macros from Ellis3D's print tuning guide. These macros provide helpful functionality for Klipper-based 3D printers.

## Macros Included

### `_CG28` (Conditional G28)
- Performs G28 homing only if the printer is not already homed
- Checks if X, Y, and Z axes are homed before executing the command

### `DUMP_VARIABLES`
- Dumps all printer variables for debugging purposes
- Supports filtering by name or value
- Parameters:
  - `NAME`: Filter variables by name (optional)
  - `VALUE`: Filter variables by value (optional)
  - `SHOW_CFG`: Whether to show config variables (default: 0)

### `GET_VARIABLE`
- Retrieves and displays a specific printer variable
- Supports nested access to complex data structures
- Parameters:
  - `NAME`: The name of the variable to retrieve (required)
  - `JOIN`: Whether to join iterable values (default: 1)

### `OFF`
- Turns off all printer functions in a single command
- Includes: steppers, heaters, cooling fans, exhaust fans, bed fans, and case lights

## Source
These macros are from Ellis3D's print tuning guide available at: https://ellis3dp.com/Print-Tuning-Guide/articles/index_useful_macros.html

## Installation
1. Add the `macros_ellis3d.cfg` file to your Klipper configuration directory
2. Include it in your printer.cfg with: `[include macros_ellis3d.cfg]`
3. Restart Klipper for the macros to become available

## Usage
- Use `CG28` in other macros where you need conditional homing
- Use `DUMP_VARIABLES` for troubleshooting and debugging
- Use `GET_VARIABLE NAME=printer.toolhead.position` to check specific values
- Use `OFF` to safely turn off the printer after printing