# Mesh2Solid

[Español](README.md) | **English**

**From a 3D mesh to a validated CAD solid, with SVG profiles for Token-style parts.**

Mesh2Solid is a desktop application for opening **STL, OBJ and 3MF** models, analysing their geometry and reconstructing solids within supported families of shapes. It focuses on two uses: **tokens and parts with stepped thickness**, including raised details, recesses or holes, and **mechanical parts** with recognisable surfaces.

The result can be exported to **STEP** for further work in CAD software. Token mode also provides **SVG profiles at actual scale** and can generate separate fill pieces for multicolour printing.

**[Download Mesh2Solid 0.1.0 for Windows x64](https://github.com/Qualith/Mesh2Solid/releases/tag/v0.1.0)** · Portable · Spanish and English interface

![Comparison of the original mesh and the reconstructed solid in Mesh2Solid](images/comparacion-malla-solido.png)

*Mechanical reconstruction example: the original mesh on the left and the validated solid on the right. Both viewport cameras are synchronised so you can compare the same area.*

## What you can do

| Feature | Purpose |
|---|---|
| **Open STL, OBJ and 3MF** | Load or drag in a mesh, check its dimensions and adjust units and scale. |
| **Analyse geometry** | Read the diagnostics, explore detected regions, and select or hide areas in the viewport. |
| **Reconstruct a solid** | Choose Automatic, Token / Extrusion or Mechanical to suit the part. |
| **Compare mesh and solid** | Inspect both models in two viewports with synchronised rotation, panning and zoom. |
| **Export STEP** | Save the solid; the application reads the file back and checks the result before accepting the export. |
| **Extract SVG profiles** | Export a profile, a tree branch, or the outline and faces A/B of each body, at a scale of 1 unit = 1 mm. |
| **Create Token fill pieces** | Generate separate pieces for supported voids and export the assembly as STEP or 3MF. |
| **Save reports** | Keep the diagnostics, reconstruction result and reasons for any rejection. |

## Token: from volume to 2D profiles

**Token / Extrusion** mode is designed for parts with a common thickness axis: tokens, plates and other models whose cross-sections remain constant within height intervals. Within its supported scope, it handles raised and recessed details on both faces, holes and multiple bodies.

After reconstruction, the **Token profiles** panel organises bodies, faces A/B and profiles in a tree, alongside a 2D drawing. You can orient each face from the outside, swap A/B and export either the selection or all profiles. If the base planes are ambiguous, you can specify their heights manually.

![Token mode showing the 3D model, face tree and 2D profiles](images/token-perfiles-svg.png)

*Example of a two-sided part with a raised detail, a recess and a hole. The profiles of face A appear on the left; the centre shows the mesh of the model that has already been reconstructed and validated.*

The fill option creates additional bodies for supported voids on face A, face B or both. The original model and fill pieces are exported as separate, aligned parts for further preparation of multicolour printing.

## Mechanical reconstruction

**Mechanical** mode extends reconstruction to supported families of planar faces, cylinders, cones, bores, chamfers and certain fillets and transitions. **Automatic** mode evaluates the available reconstruction paths and records the accepted strategy.

Acceptance depends on the geometry and the specified tolerance. When a part cannot be reconstructed within the current scope, the application displays a notice with **View reasons…** and lets you save the report. STEP export becomes available when a validated solid exists.

## Get started in a few minutes

1. Open the [latest release](https://github.com/Qualith/Mesh2Solid/releases/latest) and download **Mesh2Solid-0.1.0-Windows-x64.zip**.
2. Extract the entire ZIP and open **Release/Mesh2Solid.exe**. Keep the **app** subfolder next to the executable: it contains the application, its dependencies and their licences.
3. Open a mesh or drag an STL, OBJ or 3MF file into the window.
4. Check dimensions, units and tolerance; analyse the mesh, then reconstruct it.
5. Inspect the result and export it to **STEP**. For a Token part, also review its profiles and **SVG** options.

No development environment needs to be installed. Save your models and exports outside the application folder to preserve them when updating.

The gear in the top-right corner provides **About** information and language selection. Without a saved preference, the application starts in Spanish if the system's primary interface language is Spanish; otherwise, it starts in English. A saved language choice takes effect after restarting.

## Scope of this release

The current distribution is for **64-bit Windows**. Linux and other platforms remain pending.

- Reconstruction is limited to the implemented families of geometry; an arbitrary mesh may be rejected.
- The STEP file contains reconstructed geometry. It does not recover sketches, feature history or nominal dimensions from the original design.
- Mesh repair remains pending. Start with a mesh suitable for reconstruction and review the diagnostic notices.
- Materials, textures and printing settings from a 3MF file are not transferred to the CAD result.
- The package has been checked on the development machine using its bundled dependencies. Validation on a separate clean PC, Windows 11 and editing in Fusion remain pending.

The screenshots show the actual application from the published package, with the interface in Spanish. This release includes checks covering conversion, viewports, STEP export and languages; the published ZIP's checksum is provided in **SHA256SUMS.txt**.

## OCCT source

The [official source archive `occt-7.9.3-source.tar.gz`](https://github.com/Qualith/Mesh2Solid/raw/refs/heads/main/third-party/occt/occt-7.9.3-source.tar.gz) is available in this repository alongside the [rebuild and licensing instructions](third-party/occt/README.md).

This dependency's source is provided separately from the portable ZIP. You do not need to download it to run Mesh2Solid. Licences for bundled dependencies remain in `Release/app/licenses` inside the package.
