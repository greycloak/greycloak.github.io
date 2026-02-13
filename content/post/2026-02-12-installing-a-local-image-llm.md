---
layout: post
title: "Running Stable Diffusion Locally on Fedora 43 with no GPU"
date: 2026-02-12
thumbnail: /images/stable-diffusion.png
featureImage: /images/stable-diffusion.png
featureImageAlt: "Stable Diffusion rings"
tags: ["AI", "Stable Diffusion", "Fedora", "Linux", "Framework Laptop", "Image Generation"]
categories: ["AI", "Linux"]
draft: false
---

If you’ve got a Fedora 43 laptop (especially something like a Framework with Intel integrated graphics) and you want to generate AI images locally, you can do it — without CUDA, without NVIDIA drivers, and without the heavyweight PyTorch + AUTOMATIC1111 setup.

This guide walks through the exact steps that worked for me using:

- **stable-diffusion.cpp** (fast C++ backend)
- **sd.cpp-webui** (simple Gradio-based browser UI)
- **Stable Diffusion v1.5 safetensors model**
- **Python 3.12** (important!)

This setup is CPU-friendly and runs well on modern laptops.

## Why This Setup?

Most Stable Diffusion setups assume you have a dedicated NVIDIA GPU. If you’re running on Intel integrated graphics, AUTOMATIC1111 and ComfyUI will run, but they’re often painfully slow and can be frustrating to install.

Instead, this approach uses stable-diffusion.cpp, a lightweight inference engine written in C/C++, which runs on CPU very efficiently. Then sd.cpp-webui wraps it in a browser UI.

# Step 1: Install System Dependencies

Fedora ships Python 3.13 by default, but Python 3.13 often triggers package build problems (especially with pydantic-core, which requires Rust compilation). The easiest fix is to install Python 3.12 and build the web UI venv using that.

Install Python 3.12:

```
sudo dnf install -y python3.12 python3.12-devel
```

Also install basic tools:
```
sudo dnf install -y git curl
```

# Step 2: Clone sd.cpp-webui

Pick a working directory (I used ~/Code):
```
mkdir -p ~/Code
cd ~/Code
git clone https://github.com/DaniAndTheWeb/sd.cpp-webui
cd sd.cpp-webui
```

# Step 3: Create a Python 3.12 Virtual Environment

Remove any old venv if it exists:
```
rm -rf venv
```


Create a new venv using Python 3.12:
```
python3.12 -m venv venv
source venv/bin/activate
```


Now bootstrap pip inside the venv using ensurepip:
```
python -m ensurepip --upgrade
python -m pip install -U pip setuptools wheel
```

# Step 4: Install Python Requirements

Inside the activated venv:
```
python -m pip install -r requirements.txt
```


This should succeed cleanly (and avoids the Rust/maturin failures that can happen under Python 3.13).

# Step 5: Download the Stable Diffusion Model

Next you need actual model weights. sd.cpp-webui expects checkpoints under:

`models/checkpoints/`


The most reliable model to start with is the official SD 1.5 pruned EMA safetensors checkpoint:

Download SD 1.5 (4.27GB)
```
cd ~/Code/sd.cpp-webui/models/checkpoints

curl -L -o v1-5-pruned-emaonly.safetensors \
  https://huggingface.co/stable-diffusion-v1-5/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.safetensors
```

This resolve/main/... URL is the trick — it downloads the real binary model file, not a placeholder.

Verify the file exists:
```
ls -lh v1-5-pruned-emaonly.safetensors
```


You should see something like ~4.3GB.

# Step 6: Start the Web UI

Go back to the root folder:
```
cd ~/Code/sd.cpp-webui
```


Start the UI:
```
./sdcpp_webui.sh --autostart
```


This launches a local Gradio server. By default you can open it at:

http://localhost:7860

# Step 7: Generate an Image (Important Fix: Use CPU RNG)

On non-NVIDIA systems (Framework laptop, Intel iGPU), the UI may try to use CUDA RNG settings:

`--rng cuda --sampler-rng cuda`


Those are wrong for this system.

You want:

`--rng cpu --sampler-rng cpu`


Once set correctly, image generation works normally.

# Step 8: Testing via sd-cli (Optional but Useful)

If you want to test the backend directly (or troubleshoot), run:
```
cd ~/Code/sd.cpp-webui

./sd-cli -M img_gen \
  --model models/checkpoints/v1-5-pruned-emaonly.safetensors \
  -p "A woman holding a tennis racket" \
  --steps 20 -W 512 -H 512 \
  --sampling-method euler_a \
  --cfg-scale 7 \
  --rng cpu --sampler-rng cpu \
  -o outputs/txt2img/test.png --color
```

If successful, you’ll get:

`outputs/txt2img/test.png`

Performance Expectations on a Framework Laptop

This setup is CPU-based, so don’t expect GPU-level speed.

Typical timings on a modern laptop CPU:

* 512×512 @ 20 steps: ~2–6 minutes per image
* Higher resolutions: much slower

If you want faster iteration:

* use 256×256 or 384×384
* reduce steps to 15
* stick to SD 1.5 instead of SDXL

Summary

Here’s what made the difference:

*  Use sd.cpp-webui + stable-diffusion.cpp instead of PyTorch-based web UIs
*  Install and run everything under Python 3.12
*  Download the real checkpoint file from Hugging Face using the resolve/main URL
*  Set RNG to CPU (--rng cpu --sampler-rng cpu)
*  Generate images locally from a browser UI on Fedora with no NVIDIA GPU
