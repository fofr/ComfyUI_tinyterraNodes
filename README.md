# tinyterraNodes
A selection of custom nodes for [ComfyUI](https://github.com/comfyanonymous/ComfyUI).

<img src="https://github.com/TinyTerra/ComfyUI_tinyterraNodes/blob/main/workflows/tinyterra_trueHRFix.png?raw=true">

## Installation
Navigate to the **_ComfyUI/custom_nodes_** directory, and run:

`git clone https://github.com/TinyTerra/ComfyUI_tinyterraNodes.git`

### AutoUpdate
On the first run, a config.ini file will be created with - "autoUpdate" = false.
If you want the node pack to auto update when you start Comfy set this to true.

### Special Features
**Embedding Auto Complete**

*Enabled by default*
+ displays a popup to autocomplete embedding filenames in text widgets
+ to use start typing "embedding" and select an option from the list

**ttNstyles**

*Disabled by default - enable in the config.ini file ([ttNstyles] apply_custom_styles = True)*
+ Change the default link line type ([ttNstyles] link_type = curve | straight | direct)
+ Sets the link color for PIPE_LINE and INT (customizable within config.ini [ttNstyles])
+ Sets the default ttNode background color to black

<br>
<details open>
	<summary>$\Large\color{white}{Nodes}$</summary>
 
## ttN/image
  
<details>
  <summary>imageOutput</summary>
  
Preview or Save an image with one node, with image throughput.
+ _**Inputs -** image, image output[Preview, Save], save prefix_
+ _**Outputs -** image_
  
</details>
  
<details>
  <summary>imageRemBG</summary>
  
(Using [RemBG](https://github.com/danielgatis/rembg))

Background Removal node with optional image preview & save.
+ _**Inputs -** image, image output[Disabled, Preview, Save], save prefix_
+ _**Outputs -** image, mask_

Example of a photobashing workflow using pipeNodes, imageRemBG, imageOutput and nodes from [ADV_CLIP_emb](https://github.com/BlenderNeko/ComfyUI_ADV_CLIP_emb) and [ImpactPack](https://github.com/ltdrdata/ComfyUI-Impact-Pack/tree/Main):
![photobash](workflows/tinyterra_imagebash.png)

 </details>
  
<details>
  <summary>hiresFix</summary>

Upscale image by model, optional rescale of result image.
+ _**Inputs -** image, vae, upscale_model, rescale_after_model[true, false], rescale[by_percentage, to Width/Height], rescale method[nearest-exact, bilinear, area], factor, width, height, crop, image_output[Hide, Preview, Save], save prefix, output_latent[true, false]_
+ _**Outputs -** image, latent_
   </details>


## ttN/pipe

<details>
  <summary>pipeLoader</summary>
  
(Modified from [Efficiency Nodes](https://github.com/LucianoCirino/efficiency-nodes-comfyui) and [ADV_CLIP_emb](https://github.com/BlenderNeko/ComfyUI_ADV_CLIP_emb))

Combination of Efficiency Loader and Advanced CLIP Text Encode with an additional pipe output
+ _**Inputs -** model, vae, clip skip, (lora1, modelstrength clipstrength), (Lora2, modelstrength clipstrength), (Lora3, modelstrength clipstrength), (positive prompt, token normalization, weight interpretation), (negative prompt, token normalization, weight interpretation), (latent width, height), batch size, seed_
+ _**Outputs -** pipe, model, conditioning, conditioning, samples, vae, clip, seed_
   </details>

<details>
  <summary>pipeKSampler</summary>
  
(Modified from [Efficiency Nodes](https://github.com/LucianoCirino/efficiency-nodes-comfyui) and [QOLS_Omar92](https://github.com/omar92/ComfyUI-QualityOfLifeSuit_Omar92))

Combination of Efficiency Loader and Advanced CLIP Text Encode with an additional pipe output
+ _**Inputs -** pipe, (optional pipe overrides), script, (Lora, model strength, clip strength), (upscale method, factor, crop), sampler state, steps, cfg, sampler name, scheduler, denoise, (image output [None, Preview, Save]), Save_Prefix_
+ _**Outputs -** pipe, model, conditioning, conditioning, samples, vae, clip, image, seed_

Old node layout:

<img src="https://github.com/TinyTerra/ComfyUI_tinyterraNodes/assets/115619949/32b189de-42e3-4464-b3b2-4e0e225e6abe"  width="50%">

With pipeLoader and pipeKSampler:

<img src="https://github.com/TinyTerra/ComfyUI_tinyterraNodes/assets/115619949/c806c2e3-2efb-44cb-bdf0-3fbc20251456"  width="50%">
  </details>
  
<details>
  <summary>pipeIN</summary>

Encode up to 8 frequently used inputs into a single Pipe line.
+ _**Inputs -** model, conditioning, conditioning, samples, vae, clip, image, seed_
+ _**Outputs -** pipe_
   </details>

<details>
  <summary>pipeOUT</summary>

Decode single Pipe line into the 8 original outputs, AND a Pipe throughput.
+ _**Inputs -** pipe_
+ _**Outputs -** model, conditioning, conditioning, samples, vae, clip, image, seed, pipe_
   </details>

<details>
  <summary>pipeEDIT</summary>

Update/Overwrite any of the 8 original inputs in a Pipe line with new information.
+ _**Inputs -** pipe, model, conditioning, conditioning, samples, vae, clip, image, seed_
+ _**Outputs -** pipe_
   </details>

<details>
  <summary>pipe > basic_pipe</summary>

Convert ttN pipe line to basic pipe (to be compatible with [ImpactPack](https://github.com/ltdrdata/ComfyUI-Impact-Pack)), WITH original pipe throughput
+ _**Inputs -** pipe[model, conditioning, conditioning, samples, vae, clip, image, seed]_
+ _**Outputs -** basic_pipe[model, clip, vae, conditioning, conditioning], pipe_
   </details>

<details>
  <summary>pipe > Detailer Pipe</summary>
  
Convert ttN pipe line to detailer pipe (to be compatible with [ImpactPack](https://github.com/ltdrdata/ComfyUI-Impact-Pack)), WITH original pipe throughput
+ _**Inputs -** pipe[model, conditioning, conditioning, samples, vae, clip, image, seed], bbox_detector, sam_model_opt_
+ _**Outputs -** detailer_pipe[model, vae, conditioning, conditioning, bbox_detector, sam_model_opt], pipe_
   </details>


## ttN/text
<details>
  <summary>text</summary>

Basic TextBox Loader.
+ _**Outputs -** text (STRING)_
   </details>

<details>
  <summary>textDebug</summary>

Text input, to display text inside the node, with optional print to console.
+ _**inputs -** text, print_to_console_
+ _**Outputs -** text (STRING)_
   </details>
  
<details>
  <summary>textConcat</summary>

3 TextBOX inputs with a single concatenated output.
+ _**inputs -** text1, text2, text3 (STRING's), delimiter_
+ _**Outputs -** text (STRING)_
   </details>

<details>
  <summary>7x TXT Loader Concat</summary>

7 TextBOX inputs concatenated with spaces into a single output, AND seperate text outputs.
+ _**inputs -** text1, text2, text3, text4, text5, text6, text7 (STRING's), delimiter_
+ _**Outputs -** text1, text2, text3, text4, text5, text6, text7, concat (STRING's)_
   </details>

<details>
  <summary>3x TXT Loader MultiConcat</summary>

3 TextBOX inputs with seperate text outputs AND multiple concatenation variations (concatenated with spaces).
+ _**inputs -** text1, text2, text3 (STRING's), delimiter_
+ _**Outputs -** text1, text2, text3, 1 & 2, 1 & 3, 2 & 3, concat (STRING's)_
   </details>

## ttN/util
<details>
  <summary>seed</summary>

Basic Seed Loader.
+ _**Outputs -** seed (INT)_
   </details>

<details>
  <summary>float</summary>

float loader and converter
+ _**inputs -** float (FLOAT)_
+ _**Outputs -** float, int, text (FLOAT, INT, STRING)_
   </details>

<details>
  <summary>int</summary>
  
int loader and converter
+ _**inputs -** int (INT)_
+ _**Outputs -** int, float, text (INT, FLOAT, STRING)_
   </details>
  
 </details>
