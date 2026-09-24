# Text → SVG on free Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/EmES777/vector-svg-colab/blob/main/vector_svg_colab.ipynb)

Prompt → raster (SDXL-Turbo) → vector trace (VTracer) → downloadable SVG.
Gradio UI, three cells, runs on a free Colab T4.

## Use

1. Open the notebook via the badge above.
2. `Runtime → Change runtime type → T4 GPU`.
3. Run cell 1 (install, ~2 min), then cell 2 (model + UI, ~3 min first run).
4. Enter a prompt, tune the VTracer sliders, download the `.svg`.

## Tracing parameters

| Parameter | Effect |
| --- | --- |
| `filter_speckle` | Drops small noise shapes. Raise it when the SVG has hundreds of tiny paths. |
| `color_precision` | Number of distinct colors kept. Lower = flatter, smaller file. |
| `layer_difference` | Merges near-identical color layers. |
| `path_precision` | Decimal places in path coordinates. |
| `mode` | `spline` for smooth curves, `polygon` for hard edges, `pixel` for no tracing. |

Prompt style matters more than any slider: the notebook appends
`flat vector illustration, bold solid colors, no gradients`. Gradients and
texture turn into thousands of paths.

## FLUX.1-schnell (raster, near-Midjourney quality)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/EmES777/vector-svg-colab/blob/main/flux_schnell_colab.ipynb)

`flux_schnell_colab.ipynb` runs FLUX.1-schnell (12B) on the same free T4 using
4-bit NF4 quantization. Apache 2.0, so no HuggingFace token gate. Four steps,
~30-60 s per 1024px image, Gradio gallery with seeds and aspect ratios.

FLUX reads sentences, not tag soup. Describe the scene, the light and the lens;
drop `masterpiece, 8k, trending on artstation`.

FLUX.1-dev scores slightly higher on aesthetics but is gated behind a license
acceptance and needs a token, so schnell is the default here.

## Notes

Free Colab gives no GPU guarantee, ~12.7 GB RAM, disconnects after 90 min idle,
and caps daily GPU hours. Download results as you go.

Native SVG generation (`starvector/starvector-1b-im2svg`) fits a T4 and is worth
trying for icons. Score-distillation approaches (VectorFusion, SVGDreamer) need a
`diffvg` CUDA build that routinely fails on current Colab images — avoided here.
