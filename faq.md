[Back to Home](README.md)

<img src="assets/GSOPs_horizontal_light.png" width="240" />

# FAQ

Common questions and troubleshooting for GSOPs.

---

## My splat isn't showing up — but I can see it in Splat Transform mode. Why?

Two common causes:

**1. The splat index points to an empty slot.**
If you have, say, 3 splats loaded but the splat index is set to `3` or `4`, there's nothing at that slot. Splat Transform mode **wraps** the index (modulo the number of loaded splats), so it always shows *something* — but the particle system does **not** wrap. The result: the splat looks fine in Transform mode yet renders nothing in the actual system. Set the index to a valid loaded slot.

**2. The camera isn't framing the splat.**
The splat may simply be outside the current camera view. Check your camera position and orientation so the splat is actually in frame. Press the "Open GUI" parameter and then use the interactive camera viewport to reposition your splat

---

## I'm seeing errors and text DAT warnings on load. Is this a problem?

**No — these are cosmetic only.** They refer to internal files that are saved as text, which TouchDesigner loads without the references. Nothing actually breaks. Future releases will resolve these so the cosmetic errors are no longer surfaced.

---

## Can I use normal point clouds instead of splats with this pipeline?

**No.** Right now, only trained Gaussian splat point clouds — in `.ply` or `.spz` format — are supported. Standard point clouds lack the key attributes required for the render pipeline and will not function. This may change in future releases.

---

## How does GSOPs compare to Dan Tapper's Gaussian splat plugin, or the TouchDesigner palette Gaussian Splat component?

(These are two separate plugins — Dan Tapper's plugin and the TD palette component are not the same thing.)

GSOPs is a fully-formed, adaptable toolkit — there's a large amount of functionality on top of basic rendering that's entirely optional to use. That said, even the **free version** of GSOPs directly replicates the behavior of both, in a more approachable and more performant way.

Because GSOPs are POP-based, you can still drop any other POPs in between the operators — so there's no lost functionality, and you gain some quality-of-life improvements along the way.

---

## Is there a free version?

**Yes — GSOPs Lite is free** and includes the functionality required to load and work with Gaussian splats. With it, you can still load multiple splats, render them with one click, and reposition or switch between them.

