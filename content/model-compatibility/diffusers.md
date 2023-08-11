
+++
disableToc = false
title = "🆕 Diffusers"
weight = 4
+++

[Diffusers](https://huggingface.co/docs/diffusers/index) is the go-to library for state-of-the-art pretrained diffusion models for generating images, audio, and even 3D structures of molecules. 

![anime_girl](https://github.com/go-skynet/LocalAI/assets/2420543/8aaca62a-e864-4011-98ae-dcc708103928)
(Generated with [AnimagineXL](https://huggingface.co/Linaqruf/animagine-xl))

Note: currently only the image generation is supported. It is experimental, so you might encounter some issues on models which weren't tested yet.

## Setup

This is an extra backend - in the container is already available and there is nothing to do for the setup.

## Model setup

The models will be downloaded the first time you use the backend from `huggingface` automatically.

Create a model configuration file in the `models` directory, for instance to use `Linaqruf/animagine-xl` with CPU:

```yaml
name: animagine-xl
parameters:
  model: Linaqruf/animagine-xl
backend: diffusers

# Force CPU usage - set to true for GPU
f16: false
diffusers:
  pipeline_type: StableDiffusionXLPipeline
  cuda: false # Enable for GPU usage (CUDA)
  scheduler_type: EulerAncestralDiscreteScheduler
```

## Usage

Use the `image` generation endpoint with the `model` name from the configuration file:

```bash
curl http://localhost:8080/v1/images/generations \
    -H "Content-Type: application/json" \
    -d '{
      "prompt": "<positive prompt>|<negative prompt>", 
      "model": "animagine-xl", 
      "step": 51,
      "size": "1024x1024" 
    }'
```
