# Argus™

**A multi-height 360° camera rig for systematic interior reality capture.**

Argus mounts standard Insta360 X4 cameras at three fixed, repeatable elevations so that a single walk through a building produces the vertical coverage and even image distribution that structure-from-motion reconstruction depends on. It is built from 3D printed parts and off-the-shelf hardware at a small fraction of the cost of a commercial mobile mapping system.

Argus is the hardware half of a pair. The software half is [Hera](https://github.com/rnewbold06/Hera), which plans the capture, generates the fiducial control network, and processes the resulting footage into SfM-ready imagery.

Developed for the *Inside Out* digital twin research project at Salisbury University. An RCL Services product.

<!-- TODO: hero photo of the assembled rig, ideally in use -->
<!-- ![Argus assembled](docs/img/argus-hero.jpg) -->

---

## Contents

- [Why multiple heights](#why-multiple-heights)
- [Specifications](#specifications)
- [Bill of materials](#bill-of-materials)
- [Printing](#printing)
- [Assembly](#assembly)
- [Rig geometry](#rig-geometry)
- [Using it](#using-it)
- [CAD source and versioning](#cad-source-and-versioning)
- [Limitations](#limitations)
- [Remixing](#remixing)
- [Citing](#citing)
- [License](#license)

---

## Why multiple heights

A single 360° camera carried at chest height through a building produces a reconstruction with a characteristic set of failures. Ceilings and floors are captured at grazing angles or not at all. Every image originates from nearly the same horizontal plane, so the vertical baseline available to the bundle adjustment is close to zero, and depth estimation degrades accordingly. Furniture and counters occlude large regions that never get seen from a second angle.

Three cameras at fixed, known vertical separation fix this in one pass rather than three:

- **Vertical baseline.** Simultaneous views separated by a metre or more give the solver real parallax in the vertical axis.
- **Occlusion recovery.** The low camera sees under tables and counters; the top camera sees over them and into ceiling detail.
- **Repeatability.** Fixed elevations mean two walks of the same building are directly comparable, and the numbers you gave the planner match what you actually captured.
- **One pass.** Three separate walks at different heights cost three times the field time and introduce lighting changes between passes.

The fixed geometry is what makes the whole thing plannable. Because the elevations are known, [KapturPlan](https://github.com/rnewbold06/Hera) can compute camera heights, tag placement, and walking speed ahead of time instead of after the fact.

---

## Specifications

<!-- TODO: fill in the real numbers. Everything in this table needs verifying against the built rig. -->

| | |
|---|---|
| Cameras | 3 × Insta360 X4 (compatible with similar 360° cameras — see note below) |
| Camera separation | Top `<TODO>` mm above middle; low `<TODO>` mm below middle |
| Overall height | `<TODO>` mm |
| Mass, without cameras | `<TODO>` g |
| Mass, loaded | `<TODO>` g |
| Mount interface | `<TODO>` (e.g. 1/4-20 to camera, mast diameter) |
| Printed parts | `<TODO>` unique parts, `<TODO>` total |
| Print material | `<TODO>` |
| Non-printed hardware | See [BOM.md](BOM.md) |
| CAD source | Onshape — `<TODO: public link>` |

**Camera compatibility.** Any 360° camera with a standard 1/4-20 mount and similar body dimensions should fit the camera brackets, but the brackets are dimensioned around the X4. Other bodies will likely need the bracket remixed. If you adapt Argus to a different camera, open an issue — a variants folder is worth having.

---

## Bill of materials

Full parts list with quantities, sources, and approximate cost in **[BOM.md](BOM.md)**.

<!-- TODO: add a one-line total cost figure here once BOM.md is final. It's the most persuasive number on the page. -->

---

## Printing

<!-- TODO: fill in actual settings used. -->

| Setting | Value |
|---|---|
| Material | `<TODO>` |
| Layer height | `<TODO>` mm |
| Walls / perimeters | `<TODO>` |
| Infill | `<TODO>` % `<TODO pattern>` |
| Supports | `<TODO>` |
| Orientation | `<TODO — per part, or note in the STL folder>` |

**Notes.**

- Camera brackets carry the entire load of a camera on a moving rig. Print them with enough perimeters that layer adhesion is not the failure mode, and orient them so layer lines run across the load rather than along it.
- `<TODO: threaded insert sizes and installation notes, if used>`
- STLs live in [`stl/`](stl/) and follow the naming convention `argus2_<part>_v<N>.stl`.

---

## Assembly

Step-by-step instructions with photos in **[assembly.md](assembly.md)**.

<!-- TODO: assembly.md needs the actual steps. At minimum: order of operations, tools required, torque or tightness cautions, and how to verify the cameras end up level and coaxial. That last one matters — if the three cameras aren't vertically aligned, the fixed-offset assumption KapturPlan relies on stops holding. -->

Estimated build time: `<TODO>`

---

## Rig geometry

Hera's planner defaults describe the rig as built. Middle camera height is derived from operator height, and the other two are offsets from it:

| Position | Offset from middle | Height for a 1.78 m operator |
|---|---|---|
| Top | +0.55 m | ≈ 1.83 m |
| Middle | — | ≈ 1.28 m |
| Low | −0.75 m | ≈ 0.53 m |

Middle sits at roughly 0.72 × operator height, which puts it near sternum level for a comfortable two-handed carry. Top and low are clamped in software against ceiling height and floor.

<!-- TODO: confirm these offsets match the physical rig. If the rig is adjustable rather than fixed, say so and give the range — that changes how someone should use the planner. -->

If you build a variant with different spacing, enter your own offsets in KapturPlan rather than using the defaults. The planner's camera height output, and therefore its ceiling and floor warnings, depend on them.

---

## Using it

**1. Plan the capture** in KapturPlan: draw the space, enter your height and the rig offsets, get a walking path, tag placement, and walking speed.

**2. Print and place AprilTags** per the plan, using Hera's tag generator.

**3. Mount and start all three cameras.** Start them as close to simultaneously as possible. `<TODO: note whichever method you actually use — remote, app, voice — and any clapper or visual sync marker for aligning the three streams afterwards.>`

**4. Walk the planned path** at the planned speed. Smooth and continuous beats fast. Stop-and-go introduces motion blur at the restarts.

**5. Export equirectangular video** from each camera and feed it to Hera's three camera slots.

Field notes:

- Paint your operator mask once per rig configuration, not once per building. As long as you hold the rig the same way, the mask holds.
- `<TODO: battery life per camera under continuous 360° recording, and how many rooms that realistically covers. This is the single most useful practical number you can give someone building this.>`
- `<TODO: storage rate — GB per minute per camera at your shooting resolution.>`

---

## CAD source and versioning

Source geometry is maintained in Onshape: `<TODO: public document link>`

Exported STLs are committed to [`stl/`](stl/) using `argus2_<part>_v<N>.stl`. The repo is tagged whenever STLs change, so an external listing (Thingiverse, Printables) can point at a specific commit rather than drifting from source.

**If you change a part**, bump its `_v<N>`, re-export, commit, and tag. Do not overwrite an STL in place — someone may have printed the old one and needs to know which version their hardware matches.

---

## Limitations

Stated plainly, because a hardware repo that only lists strengths is not useful to anyone deciding whether to build it.

- **Not survey-grade.** Argus produces imagery for photogrammetric reconstruction. Absolute accuracy depends on your control network and scale constraints, not on the rig. It is not a substitute for a laser scanner or a total station, and nothing it produces constitutes a boundary survey or a certified as-built.
- **No synchronised triggering.** `<TODO: confirm.>` Cameras are started individually, so the three streams need aligning in post.
- **Handheld.** Motion blur is the dominant image quality constraint. Walk smoothly, keep the shutter fast, and use Hera's blur gate.
- **Interior-oriented.** The geometry is designed for room-scale interiors with a ceiling overhead. Outdoor use works but the top camera's advantage largely disappears.
- **Printed parts are the weak point.** Treat bracket failure as a when, not an if, and carry a spare on long jobs.

---

## Remixing

Argus is CC BY 4.0. Build it, modify it, adapt it to a different camera, sell prints of it. The only requirement is attribution.

If you build one, an issue with a photo and any changes you made would be genuinely useful, and variants for other camera bodies are welcome as pull requests.

---

## Citing

<!-- TODO: add a CITATION.cff to this repo the way Hera has one, so academic users can cite the hardware. -->

If Argus contributes to published work, please cite the repository and note the commit or tag corresponding to the parts you printed.

---

## Related projects

- **[Hera](https://github.com/rnewbold06/Hera)** — capture planning, AprilTag generation, and SfM preprocessing for this rig
- *Inside Out* — digital twin research, Department of Geography and Geosciences, Salisbury University
- [RCL Services](https://sites.google.com/view/rclservices/home) — Rusty's Creation Lab

---

## License

Creative Commons Attribution 4.0 International (CC BY 4.0). See [LICENSE](LICENSE).

Argus™ is a product of Rusty's Creation Lab (RCL) Services, developed independently and not affiliated with or endorsed by any institution.

© 2026 Rustin C. Newbold
