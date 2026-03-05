*This project has been created as part of the 42 curriculum by aokhapki and bszikora.*

# cub3D

## Overview
`cub3D` is a small real-time 3D renderer built with the raycasting technique.  
It is primarily a **raycast engine rather than a game**: the project focuses on map parsing, validation, textured wall rendering, and movement/camera logic.

## Platform Compatibility
- Linux

## Authors
- [Alima-T](https://github.com/Alima-T) — 42 username: `aokhapki`
- [chamaselion](https://github.com/chamaselion) — 42 username: `bszikora`

## External Dependencies
The repository includes `LIBFT` as an internal dependency, while the following tools/libraries are required externally:

- `gcc` (or another compatible C compiler)
- `make`
- `cmake` (used to configure/build MLX42)
- GLFW development package (for example `libglfw3-dev` on Debian/Ubuntu)
- System libraries linked by the build: `libm`, `pthread`, `dl`

`MLX42` is fetched and built automatically by the `Makefile` if the `MLX42/` directory is missing.

## Build Instructions
From the project root:

```bash
make
```

This compiles:
- `MLX42` (auto-cloned and built when needed)
- `LIBFT`
- the `cub3D` executable

### Make Targets
- `make` - build project
- `make clean` - remove object files
- `make fclean` - remove objects and executable
- `make re` - full rebuild
- `make cleanmlx` - remove the `MLX42/` directory

## Run Instructions
The program expects exactly one argument: a `.cub` map file.

```bash
./cub3D path/to/map.cub
```

Example:

```bash
./cub3D maps/map.cub
```

## Controls
- `W`, `A`, `S`, `D` - movement
- `Left Arrow` / `Right Arrow` - camera rotation
- `ESC` or window close button - exit

## Map File Format (`.cub`)
The map file must:
- end with the `.cub` extension
- contain all six configuration entries:
  - `NO <path>` (north texture)
  - `SO <path>` (south texture)
  - `WE <path>` (west texture)
  - `EA <path>` (east texture)
  - `F R,G,B` (floor color)
  - `C R,G,B` (ceiling color)
- contain exactly one player spawn marker: `N`, `S`, `E`, or `W`
- use valid map characters (`0`, `1`, `N`, `S`, `E`, `W`, spaces)
- represent a closed map (open walls are rejected during validation)

RGB values must be integers in the range `0-255`.

## Changing Textures (Current or New Maps)
To change wall textures for the current map or any new map:

1. Add your texture files (PNG is expected by the current texture-loading code) to a location accessible at runtime, e.g. `textures/`.
2. Edit the target `.cub` file and update `NO`, `SO`, `WE`, and `EA` entries to point to your files.
3. Run the program with that map.

Example configuration:

```text
NO ./textures/north.png
SO ./textures/south.png
WE ./textures/west.png
EA ./textures/east.png
F 80,0,0
C 10,10,30
```

Notes:
- Relative paths are supported (for example `./textures/wall.png`).
- Trailing whitespace/newlines in texture paths are trimmed by the parser.
- If a texture cannot be loaded, startup fails with an error message.

## Project Structure (High-level)
- `sources/main/` - game loop, movement, raycasting, rendering, texture sampling
- `sources/parsing/` - `.cub` parsing and RGB/texture config processing
- `sources/validation/` - map character and wall-closure checks
- `LIBFT/` - utility library
- `MLX42/` - graphics library

## Notes
This implementation targets educational goals of the 42 curriculum and emphasizes rendering fundamentals and robust map validation over advanced gameplay features.
