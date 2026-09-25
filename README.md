# llama.cpp (PrismML Extension for LM Studio)

> [!IMPORTANT]
> This repository provides **pre-compiled PrismML `llama.cpp` runtimes for LM Studio**, packaged as drop-in backend extensions for **Windows**. It allows you to **run PrismML Bonsai 1-bit / ternary GGUF models directly in LM Studio**, including models such as `*-PQ2_0.gguf` and `*-Q2_0_g64.gguf`.
>
> **Stock LM Studio `llama.cpp` runtimes do not include the custom PrismML kernels required by these ternary/Bonsai models.** If LM Studio cannot load a PrismML Bonsai model, use the corresponding PrismML runtime provided by this repository instead.
>
> **No compilation is required.** Download the appropriate pre-built runtime from [Releases](../../releases), extract it, and install the backend into `%USERPROFILE%\.lmstudio\extensions\backends\`. Look at Quick Start for a full guide.

<div align="center">

# llama.cpp (LM Studio Runtime)

**Pre-built PrismML runtime packages for instant LM Studio integration**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20x64-lightgrey.svg)](../../releases)
[![Target](https://img.shields.io/badge/Target-LM%20Studio%20Extensions-purple.svg)](https://lmstudio.ai/)

[Releases](../../releases) &bull; [Request a Build](../../issues) &bull; [Upstream PrismML](https://github.com/PrismML-Eng/llama.cpp)

</div>


## Description

Standard LM Studio releases bundle upstream `llama.cpp` builds that do not include the custom low-bit quantization kernels required to execute PrismML's Bonsai ternary architectures. Attempting to load these models on stock runtimes causes load failures or crashes.

Building the PrismML fork with proper CUDA dll files and all the other required files can be tedious and doesn't always work. This repository contains ready-to-drop backend distributions directly packaged for LM Studio's runtime architecture.

It does not break, delete or overwrite old LM Studio Files. It just adds another Runtime you can select in the settings. It is made to work directly in LM Studios GUI without needing to use the demo server made by PrismMl.

---

## Supported Backends

| Backend | Platform | Target Devices | Build Availability |
| :--- | :--- | :--- | :--- |
| **CUDA 13.3 (13.4)** | Windows x64 | NVIDIA RTX Series | Available in [Releases](../../releases) |
| **CUDA 12.x** | Windows x64 | NVIDIA GTX / RTX Series | On request |
| **CPU / AVX2** | Windows x64 | x86_64 CPUs | In work |

---
---

## Quick Start

### 1. Download the Release
Download the latest `.zip` archive matching your CUDA environment from the [Releases](../../releases) tab.

The archive contains an LM Studio runtime folder structured similar to:
```text
llama.cpp-prism-b<build>-<commit>-bin-win-cuda-<version>-x64-lm-studio
```
*(Exact naming varies by build, e.g. `llama.cpp-prism-b10709-9a9394a-bin-win-cuda-13.3-x64-lm-studio`)*.

### 2. Install to LM Studio Backends
1. Extract the downloaded `.zip` file.
2. Copy the inner folder directly into LM Studio's backend extensions directory:

```text
C:\Users\<Username>\.lmstudio\extensions\backends\
```

> **Shortcut:** Press `Win + R`, paste `%USERPROFILE%\.lmstudio\extensions\backends`, and press Enter.

Your directory layout should look like this:
```text
C:\Users\<Username>\.lmstudio\extensions\backends\
└── llama.cpp-prism-...-lm-studio\
    ├── ... (binaries, runtime files, package metadata)
```

### 3. Activate in LM Studio
1. Start (or restart) **LM Studio**.
2. Open **Settings** (gear icon) and go to **Runtime**.
3. Under the **GGUF** section, select the newly added runtime:
   ```text
   Prism ML Cuda xx.x llama.cpp (Windows)
   ```
4. Load your PrismML Bonsai ternary model and run inference.

---

## Requesting a Build or Version

If you need a release variant that is not currently uploaded (such as a specific CUDA version, an AVX2 CPU-only package, or an update tracking a newer PrismML commit):

1. Go to the [Issues](../../issues) tab of this repository.
2. Open a **New Issue**.
3. Set the title to something like `Build Request: <CUDA version / Arch / Commit>`.
You can find all versions that can be requested to be precompiled for LM Studio in [PrismML-Eng/llama.cpp/releases](https://github.com/PrismML-Eng/llama.cpp/releases/tag/prism-b10709-9a9394a)
> [!IMPORTANT]
> Requests for versions that are not able to be run on Windows with an RTX Series GPU or x86_64 CPUs will not be fulfilled as i do not have the hardware to test such. Not all versions listed can certainly be used in LM Studio. On request it will be checked if it works or not. 

---

## Notes & Troubleshooting

* **Runtime does not appear in LM Studio:** Ensure you copied the backend directory itself into `.lmstudio\extensions\backends\`, not nested folders or standalone loose files. A full restart of LM Studio is required to refresh backend detection.
* **Driver requirements:** Ensure your NVIDIA display driver supports the CUDA version specified in the release title.

---

## Credits

* PrismML fork and ternary kernels: [PrismML-Eng/llama.cpp](https://github.com/PrismML-Eng/llama.cpp)
* Base inference runtime: [ggml-org/llama.cpp](https://github.com/ggml-org/llama.cpp)
* Desktop environment: [LM Studio](https://lmstudio.ai/)
