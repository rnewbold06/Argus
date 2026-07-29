# Assembly

<!-- TODO: This file needs the real procedure. The structure below is the target.
     Photograph each step as you build the next one — retroactive assembly
     photos are always worse than in-progress ones. -->

**Estimated build time:** `<TODO>`
**Difficulty:** `<TODO>`

Before starting, confirm you have everything in [BOM.md](BOM.md) and that all
printed parts came off the bed clean, with no warping at the mounting faces.

---

## 1. Prepare printed parts

`<TODO: deburring, threaded insert installation, test fits>`

---

## 2. `<TODO: step name>`

`<TODO>`

<!-- ![Step 2](docs/img/assembly-02.jpg) -->

---

## 3. `<TODO: step name>`

`<TODO>`

---

## Verification

Do not skip this. KapturPlan assumes the three cameras sit at fixed, known
elevations on a common vertical axis. If that assumption is violated, every
plan it produces is subtly wrong and the error will not be obvious until
reconstruction.

Check, with the rig assembled and cameras mounted:

1. **Vertical alignment.** All three cameras coaxial. `<TODO: how to check —
   plumb line, straightedge, phone level app?>`
2. **Camera separation.** Measure top-to-middle and middle-to-bottom lens
   centre distances. Compare against the offsets in [README](README.md#rig-geometry).
   If they differ, use your measured values in KapturPlan, not the defaults.
3. **Level.** Each camera level in both axes when the rig is held upright.
4. **Rigidity.** Grip the rig by the handle and shake it. Any bracket that
   flexes visibly will produce inconsistent geometry between rooms.

Record your measured offsets somewhere you will find them again. They are an
input to every capture you plan.

---

## Field maintenance

- `<TODO: what loosens over a day of walking, what to check between buildings>`
- Carry a spare camera bracket. Printed parts fail eventually, and they fail
  at the mount.
