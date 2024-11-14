# Image Generation Worflow - All in One

# Description
The goal of this project is to create a highly customizable, locally hosted AI image generation tool. Using ComfyUI, a flexible interface for deploying diffusion models, the project allows the integration of various models such as Stable Diffusion and Flux, along with LoRA (Low-Rank Adaptation) for fine-tuning. Customization options include hyperparameter adjustments and advanced configurations, giving users full control over the quality, speed, and aesthetic characteristics of the generated images. The main model, an optimized version of Stable Diffusion XL, was chosen for its faster performance, providing a powerful and adaptable solution for AI-driven image creation.

# Table of Contents 
- [Image Generation Worflow - All in One](#image-generation-worflow---all-in-one)
- [Description](#description)
- [Table of Contents](#table-of-contents)
- [Installation \& Configuration](#installation--configuration)
- [Precondition](#precondition)
- [Structure \& Description of the workflow](#structure--description-of-the-workflow)
    - [Prompt Generator](#prompt-generator)
    - [Classic image generator](#classic-image-generator)
    - [Upscale](#upscale)
    - [Image modification](#image-modification)
    - [Pattern](#pattern)
    - [Painting](#painting)
    - [Sketch](#sketch)
- [Results \& Save](#results--save)

# Installation & Configuration

**Download ComfyUI:**

Visit the [ComfyUI GitHub page](https://github.com/comfyanonymous/ComfyUI) to access the latest version.
Choose the portable version (in .7z format) and download it to your machine.

**Extract the Archive:**

Create a folder for ComfyUI in your desired location (e.g., on the D:\ drive in a folder named ComfyUI).
Extract the contents of the .7z archive into this folder using a tool like 7-Zip or WinRAR.

**Read the README File:**

Open the README file located in the ComfyUI folder to get details on the different executable files (.bat) and configuration options.

**Launch ComfyUI with Nvidia GPU:**

Double-click the ``Run_Nvidia_GPU.bat`` file to launch ComfyUI using your Nvidia GPU (this provides faster processing).
A command window will open, displaying information about your graphics card, including VRAM and RAM capacity.

**Access the ComfyUI Interface:**

Once the process is complete, a new browser window will automatically open to display the ComfyUI interface.

**Install ComfyUI Manager**

Visit the [GitHub page for ComfyUI Manager](https://github.com/ltdrdata/ComfyUI-Manager) to access the manager tool. It simplifies the installation of workflows created by others and adds custom nodes.

Go to the ComfyUI folder you previously installed.

Navigate to the custom_nodes subfolder.

Copy the command provided in the GitHub instructions (like ``git clone https://github.com/ltdrdata/ComfyUI-Manager.git``) and paste it into the terminal.

Relaunch ComfyUI. During the restart, ComfyUI Manager will run some initial setup tasks, such as installing necessary dependencies.

# Precondition

**Custom nodes**

- ComfyUI_Comfyroll_CustomNodes
- comfyui_controlnet_aux
- ComfyUI-Crystools
- ComfyUI-Easy-Use
- ComfyUI-Florence2
- ComfyUI-GGUF
- ComfyUI-Inpaint-CropAndStitch
- ComfyUI-iTools
- comfyui-ollama
- ComfyUI-seamless-tiling
- ControlAltAI-Nodes
- rgthree-comfy
- was-node-suite-comfyui
    - in was_suite_config.json, precise the path of the style.csv in "webui_styles"

**checkpoints**

- Juggernaut_X_RunDiffusion.safetensors
- wildcardxXLANIMATION_wildcardxXLANIMATION.safetensors
- juggernautXL_versionXInpaint.safetensors

**clip**

- clip_l.safetensors 
- t5-v1_1-xxl-encoder-Q5_K_M.gguf
controlnet
- diffusion_pytorch_model_promax.safetensors

**llm**

- thwri/CogFlorence-2.2-Large
- Florence-2-base
- Florence-2-large-PromptGen-v1.5
- Florence-2-SD3-Captioner

**lora**

- glowneon_xl_v1.safetensors
upscale_models
- 4x_foolhardy_Remacri.pth
- 4x_NMKD-Siax_200k.pth
- 4x-AnimeSharp.pth
- 4x-ClearRealityV1.pth

**vae**

- ae.safetensors

# Structure & Description of the workflow

### Prompt Generator

- **Generate a prompt from a text**

![image](https://github.com/user-attachments/assets/7b81feb0-7641-49a0-9d1b-7c318472ff95)

**Goal**

The purpose of this workflow is to transform a simple idea into a richly detailed and artistic image prompt, which can be used to generate high-quality images via AI. It takes a basic scene idea and enriches it with visual details, artistic style, colors, lighting effects, and specific elements to add depth and realism to the scene.

**Inputs**

The context serves as the starting point, where the input is a concept or basic scene idea that will be developed. For instance, entering "a cute bunny next to a river" will be expanded into a detailed description of the desired image.

**Outputs**

The response is the final output, containing the fully developed prompt. This includes a comprehensive description of the original scene, with composition elements, artistic styles, and visual details that enhance the image.

**Modifiable Parameters**

*Model:*

By default, the model used is llama3.2:3b, but it can be switched to other models compatible with ComfyUI, potentially influencing the style and complexity of the generated text.

*Initial Concept (context):*

The basic scene idea text can be customized to any other subject or scene.

- **Generate a prompt from an existed image**

![image](https://github.com/user-attachments/assets/dfc62194-74bd-4dec-8172-6ec50abe2a43)

**Goal**

This workflow takes an uploaded image and generates a detailed caption or description for it, capturing elements such as the scene, objects, and visual style. It leverages the Florence-2 model to analyze the image content and produce a natural language description.

**Inputs**

The primary input is an image file, which can be uploaded in various formats. This image serves as the basis for the Florence-2 model’s analysis.

**Outputs**

The output is a descriptive caption created by the Florence-2 model. This caption provides a detailed textual representation of the image, including objects, styles, and scene details.

**Modifiable Parameters**

*Model Variant:*

The model variant (here set to ``CogFlorence-2.2-Large``) can be adjusted to other versions if available, which might affect the caption quality and level of detail.

*Output Detail Level:*

Ithe task parameter allows you to select the level of detail for the generated caption. This setting adjusts the description's complexity and specificity, enabling you to tailor the output according to your needs. ``more_detailed_caption`` is set by default for more details.

### Classic image generator

- **Basic generation**

![image](https://github.com/user-attachments/assets/fe6715d4-b0fe-44d2-9385-8f8ccd63e1e8)

**Goal**

The goal is to generate images based on text prompts, allowing the user to select from multiple styles to influence the final image's look and feel. This workflow leverages various nodes to load a model, apply positive and negative prompts, add styles, and finally output the generated image.

**Inputs**

*Positive/Negative Prompts:* Describe what elements the image should have (positive) and what it should avoid (negative).

**Outputs**

*Generated image:*

The workflow outputs a final image after decoding from the latent space, saved through the SaveImage node.

**Modifiable Parameters**

*Model Choice:*

You can load different models by changing the model name in CheckpointLoader (e.g., ``Juggernaut_X_RunDiffusion.safetensors``).

*Resolution:*

Defined by width and height in the EmptyLatentImage node, allowing for 1024x1024 or other custom dimensions.

*Prompt Style:*

Users can choose from various style options to alter the visual style.

*Sampling Steps:*

In KSampler, steps can be modified to affect image quality.

*Positive/Negative Prompts:*

Specific text inputs that shape the subject matter and attributes of the generated image.

- **With watermark or overlay**

![image](https://github.com/user-attachments/assets/f5839b04-2c8a-41de-a8d1-aeb749694c05)

**Goal**

The goal of this workflow is to create images based on text prompts that describe scenes, characters, or objects, enhanced with specific styles and overlays. It allows customization of styles and the addition of overlays for branding or watermarking.

**Inputs**

*Positive and Negative Prompts:*

Provided in the iToolsPromptStylerExtra node, where users can enter detailed descriptions of the desired image characteristics (positive prompts). Negative prompts are generated by selected styles.

*Model Selection:*

The CheckpointLoaderSimple node loads a specified model (Juggernaut_X_RunDiffusion in this case), which affects the style and quality of the generated image. The choice of model can be modified to achieve different artistic results combined with styles.

*Overlay Settings (Optional):*

The iToolsAddOverlay node takes text, color, transparency (alpha), and other overlay settings to add a watermark or annotation over the image.

**Outputs**

*Final Generated Image:*

After passing through the style settings and prompt encodings, the image is generated by the model and decoded from latent space using the VAEDecode node.

*Image with Overlay:*

An optional overlay or watermark can be applied to the image before saving, allowing for branding or protection against unauthorized use.

**Modifiable Parameters**

*Styles:*

The iToolsPromptStylerExtra node allows users to select different style templates (e.g., "Studio Ghibli") and moods, significantly affecting the output's look and feel.

*Text Content:*

Custom text can be added to the overlay.

*Font Size, Color, and Transparency:*

These settings allow fine-tuning of the watermark appearance, including transparency via the alpha channel (e.g., “blackAAFF” for semi-transparent black).

*Positioning and Font Style:*

Additional adjustments for overlay positioning and text font can be configured.

- **Use a LoRA**

![image](https://github.com/user-attachments/assets/98b579d9-f425-465c-bfe6-2792146fbdb8)

**Goal**

This workflow is designed to generate custom images using a LoRA (Low-Rank Adaptation) model in ComfyUI. It takes descriptive prompts as inputs, uses specific image generation settings, and outputs a stylized image based on these configurations. The main goal is to enable users to create images with distinctive characteristics by applying various customization options, like prompts, models, and visual styles.

**Inputs**

*Positive Prompt:*

Describes the desired content of the image. This prompt helps the model understand the scene or elements to include.

*Negative Prompt:*

Specifies elements to avoid in the image (e.g., “ugly, watermark”), helping refine the output by excluding undesired features.

*LoRA Model and Main Model:*

The workflow uses a base model (Juggernaut_X_RunDiffusion) and a LoRA model (glowneon_xl_v1.safetensors) to achieve the specified visual style. You can use any LoRA wich is compatible with the model used.

*Image Size:*

Defined in the workflow as 1024x1024, this parameter controls the resolution of the generated image.

**Outputs**

*Generated Image:*

The final image, created based on the prompts and settings

**Modifiable Parameters**

*LoRA Model:*

Select different models for varied artistic effects or styles.

*Main Model:*

Swap the base model to change the general approach to image generation.

- **Try a flux model (Schnell)**

![image](https://github.com/user-attachments/assets/28d67b37-c4d1-46f0-87c6-e7af6bd4705e)

**Goal**

The main goal of this workflow is to produce images like the first image generation workflow but based on flux models.

**Inputs**

*Positive and Negative Prompts:*

Provided in the txt2img with styles node, where users can enter detailed descriptions of the desired image characteristics (positive prompts) and what it should avoid (negative).

*Style Selector:*

This allows users to select specific styles from a list that modifies the appearance of the generated image based on predefined stylistic influences.

**Outputs**

*Generated Image:*

The primary output is the generated image based on the text prompt and selected style.

**Modifiable Parameters**

*Style Choices:*

Users can select from predefined styles, which adjust the output appearance to match particular artistic influences or visual characteristics.

*UNet Model:*

Defines the core generative model used for processing. By default : flux1-schnell-Q5_K_S.gguf

*DualCLIP Loader:*

This component loads the CLIP model to condition the text prompt, helping the model understand the semantic context of the prompt. By default : t5-v1_1-xxl-encoder-Q8_0.gguf, clip_l.safetensors, flux


### Upscale

- **Upscale an image**

![image](https://github.com/user-attachments/assets/83492600-0067-4924-a2fd-723e977ca95e)

**Goal**

The goal of this workflow is to upscale input images, improve clarity, and apply selective modifications to details based on user preferences. It’s particularly well-suited for processing images with complex or sharp details, such as anime or vector-style graphics.

**Inputs**

*Uploaded Image:*

This is the initial input image to be processed. Users can upload an image file, and this node serves as the source image for the upscaling and enhancement pipeline.

**Outputs**

*Upscaled Image Variants:*

The workflow generates multiple output images, which are saved through SaveImage nodes. These images include:
- An initial upscaled version (x2 pixels)
- A higher-quality version (x4 pixels)

**Modifiable Parameters**

*Upscaling model:*

Allows users to choose different upscaling strengths depending on the image's detail requirements.

for anime, vector, clean designs use 4x-AnimeSharp.

Else : 4x_NMKD-Siax_200k

### Image modification

- **Impose spatial conditions (ControlNet)**

![image](https://github.com/user-attachments/assets/bfd60888-33e0-4357-a821-d34640882e6e)

**Goal**

The goal of this workflow is to generate and modify images based on text prompts, using multiple preprocessing and control networks. It allows users to fine-tune results by combining different styles or effects, such as edges and depth, to control how the AI interprets various aspects of the image.

**Inputs**

*Text Prompts:*

Two prompts (positive and negative) influence image content and quality, including desired features or avoided artifacts.

*Image Control Layers:*

Optionally, multiple control layers (e.g., Canny edge, depth preprocessor) are provided as inputs.

**Outputs**

*Generated Image:*

The final output image is saved after passing through the control stack, model sampling, and decoding.

**Modifiable Parameters**

*ControlNet Layers:*

Users can select and activate different control layers (e.g., edge detection, depth processing), with options to mix and match up to three controls at once.

- **Merge 2 images**

![image](https://github.com/user-attachments/assets/1ae16c29-5a01-40be-89ae-1d8c6c065e22)

**Goal**

This workflow aims to generate a new image based on an uploaded one by leveraging an image-to-image pipeline, which enhances and alters the source image while preserving key characteristics.

**Inputs**

*Image:*

The uploaded image serves as the primary input.

*Text Prompts:*

Positive and negative prompts guide the transformation by detailing desired features.

*Model Checkpoint:*

The model file, Juggernaut_X_RunDiffusion.safetensors, defines the generative model to be used for the transformation.

**Outputs**

*Transformed Image:*

The final output is a modified image saved.

**Modifiable Parameters**

*Prompt Strength (denoise):*

A value between 0 and 1. This affects how closely the output image follows the uploaded image. Lower values retain more of the original, while higher values allow more transformation. A good starting value is 0.65.

- **Use a cartoon model**

![image](https://github.com/user-attachments/assets/a8758a95-099d-40c5-984d-14eea23a3835)

**Goal**

The workflow aims to convert an uploaded image into a cartoon-style render using a specific Stable Diffusion XL model and various preprocessing and conditioning techniques to achieve high-quality outputs.

**Inputs**

*Uploaded Image:*

The user provides an input image to be processed.

*Positive Prompts:*

Descriptive text for the desired cartoon style and features (e.g., "3D cartoon art style, vibrant colors"). Description of the image with many details.

*Aspect Ratio:*

Customizable dimensions for the output image.

**Outputs**

*Cartoon-Style Image:*

The processed image with a cartoon effect based on the provided prompts.

*Comparison Preview:*

A side-by-side comparison of the original and final images.

**Modifiable Parameters**

*Resolution:*

Width and height can be defined for the output (e.g., 1024x1024).

*Denoise Strength:*

Controls the amount of change applied to the image, typically between 0.45 and 0.85.

*Preprocessors:*

Various algorithms (e.g., line art extraction) for initial image modifications.

*ControlNet Settings:*

Includes specific model settings and strength percentages for precise control.

### Pattern

- **Create a seamless pattern**

![image](https://github.com/user-attachments/assets/f3203775-1baa-4860-ae28-c3107b71b0d9)

**Goal**

The goal is to create a seamless tile pattern, which can be repeated without visible borders. The workflow refines the generated pattern by applying both positive and negative prompts, removing unwanted artifacts, and ensuring seamlessness.

**Inputs**

*Model:*

This is the primary image generation model (in this case, ``Juggernaut_X_RunDiffusion.safetensors``) that powers the workflow.

*Positive Prompt:*

A detailed text description that specifies the desired image features, including the look and style of the leaves and background.

*Latent Image Input:*

The initial latent image dimensions (set to 1024x1024), serving as a placeholder for the pattern generation.

**Outputs**

*Seamless pattern:*

The final output is a high-resolution image which is the main seamless pattern.

*Intermediate Images:*

Additional outputs are saved to observe the image at different stages. This is helpful for debugging or comparing intermediate results.

**Modifiable Parameters**

*Image Dimensions:*

You can adjust the size of the generated pattern by changing the width and height. By default, this is set to 1024x1024.

### Painting

- **Change a part of the image**

![image](https://github.com/user-attachments/assets/3a6b8789-e3ff-4410-92f9-345d9cd5ff9d)

**Goal**

The workflow’s main purpose is to generate customized image edits through inpainting, where portions of the image are selectively modified. This enable the creation of visually appealing outputs tailored to specific requirements.

**Inputs**

*Image:*

The original image to modify.

*Mask:*

The mask defining which regions to inpaint.

*Prompts:*

Text prompts for positive and negative conditioning.

**Outputs**

*Final Image:*

The reconstructed image with inpainted areas.

*Preview:*

Previews available at different stages, including cropped and final images.

*Comparison:*

Allows comparison between the original and inpainted versions.

**Modifiable Parameters**

*Output Resolution:*

Adjusts the size of the cropped image, typically set between 512x512 and 1024x1024.

*Interpolation Method:*

Controls the resizing algorithm (e.g., bicubic or nearest).

*Prompts:*

Modify text prompts to change the features, style, or characteristics of the inpainted content.

- **Expand the image**

![image](https://github.com/user-attachments/assets/db840aad-255b-4b7b-9512-2a62ef850f38)

**Goal**

The workflow aims to generate a completed version of an image by expanding the original image.

**Inputs**

*Image:*

The main image where parts are to be inpainted.

*Mask:*

The mask image specifying the areas to be filled.

*Prompts:*

Text inputs for conditioning, which help guide the inpainting model on what should be added in the generated area.

**Outputs**

*Generated Image:*

The inpainted image is the main output, where the masked region is filled in with content generated by the model based on the prompts.

*Preview Images:*

A comparison is provided between the original image and the inpainted result.

*Saved Image:*

The final output image is saved.

**Modifiable Parameters**

*Prompt:*

Adjust the description of the desired for more control over the inpainting content.

*rop and Resize Options:*

In the InpaintCrop node, adjust how the input image is resized and cropped before being processed, affecting the resolution and the area being inpainted.

### Sketch

- **Preparation**

![image](https://github.com/user-attachments/assets/24decd19-c7b2-4d4a-af9c-8b44021eeb93)

**Goal**

The objective of this workflow is to prepare, edit, and enhance an image, using multiple stages that include resizing, aspect ratio adjustments, filter enhancements, and a side-by-side comparison of the original versus the edited image. It offers users a streamlined process to load an image, configure its dimensions and filters, and then save or review the final output.

**Inputs**

*Input Image:*

An image file loaded through the LoadImage node. This serves as the base image to which all subsequent edits are applied.

**Outputs**

*Edited Image Preview:*

A visual preview of the resized and cropped image is available before any adjustments are applied (through Preview Image after Crop and Resize).

*Final Edited Image:*

Saved through the SaveImage node, allowing users to retain a final version with all applied edits.

*Comparison Display:*

A split view in the Image Comparer node to visually compare the original versus edited image, useful for evaluating enhancements.

**Modifiable Parameters**

*Aspect Ratio & Resolution:*

Set via the FluxResolutionNode, where users select the desired width and height, either as fixed values or common aspect ratios.

*Filter Adjustments:*

Users can modify brightness, contrast, saturation, and edge enhancement through the Image Filter Adjustments node to achieve the desired level of enhancement.

- **Variation**

![image](https://github.com/user-attachments/assets/b3530412-abc4-4b88-8e0e-1154553d4e38)

**Goal**

This workflow aims to generate highly detailed images based on a sketch. The system also allows for aspect ratio adjustments and noise control during the denoising phase to balance the quality and style of the final output. This tool is ideal for users who wish to create complex, high-resolution artwork with adjustable parameters to tailor results closely to their vision or have inspiration.

**Inputs**

*Uploaded Image:*

An initial image that can guide the model for certain types of outputs.

*Positive Prompt:*

Describes the desired details.

**Outputs**

*Generated Image:*

An image with the characteristics defined by the prompts and scaling options.

*Comparison Output:*

Allows for side-by-side comparison of the original and modified images, facilitating visual tuning.

**Modifiable Parameters**

*Resolution Scaling:*

Aspect ratio settings (e.g., 4:3, 1:1) let users fit the generated image to their preferred frame size.

*Noise Control:*

Denoising levels can be adjusted to either preserve more detail or create smoother transitions.

- **Generate an image from a Sketch**

![image](https://github.com/user-attachments/assets/1276ce52-50b7-4f44-abd4-ef62af8bae78)

**Goal**

This workflow transforms a user-provided sketch into a fully detailed image using ControlNet with SDXL. It applies various preprocessing techniques to enhance the sketch and generate a refined output based on text-based prompts.

**Inputs**

*Uploaded Sketch:*

A user-provided sketch or image serves as the base input.

*Positive Prompts:*

Detailed text descriptions specifying the desired appearance of the generated image.

*Aspect Ratio:*

Customizable dimensions that match the proportions of the uploaded sketch.

**Outputs**

*Generated Image:*

A detailed image based on the uploaded sketch and user-provided prompts.

*Comparison View:*

A side-by-side comparison of the original sketch and the final image to evaluate transformations.

**Modifiable Parameters**

*Preprocessors:*

Choose preprocessing algorithms (e.g., Canny Edge Detection, Line Art).

*Denoise Strength:*

Adjusts how much of the sketch's original content influences the output (range: 0.3–1.0). A lower value emphasizes creativity, while a higher value ensures fidelity to the sketch.

*ControlNet Settings:*

Control parameters like strength (e.g., 0.8) for precise adjustments to the transformation process.

- **Generate an image from a drawing**

![image](https://github.com/user-attachments/assets/bda78d31-b845-4c4e-a504-1db00c475ff8)

**Goal**

The primary objective is to create a detailed and high-quality image from a textual prompt while using additional conditioning to guide the model’s output. The workflow integrates text prompts, input image processing, and advanced AI models (like ControlNet) to ensure the generated image meets the desired criteria, such as following specific shapes, structures, or themes.

**Inputs**

*Prompt:*

Describes the desired elements or features to be included in the generated image.

*Output Resolution:*

Adjusts the size of the image.

*Drawing:*

Click on edit and draw the shape you want.

**Outputs**

*Generated Image:*

An image with the characteristics defined by the prompts, scaling options and the drawing.

*Comparison Output:*

Allows for side-by-side comparison of the original and modified images, facilitating visual influence of the drawing.

**Modifiable Parameters**

*Output Resolution:*

Adjusts the size of the cropped image, typically set between 512x512 and 1024x1024.

*Prompts:*

Modify text prompts to change the features, style, or characteristics of the inpainted content.

*AIO_Preprocessor:*

Try different preprocessors to have multiple results.

# Results & Save

All the images generated are saved in the ``output`` folder.
