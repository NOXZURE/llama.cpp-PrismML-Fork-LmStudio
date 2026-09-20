# llama.cpp (PrismML Backend for LM Studio)

Pre-built binaries of the [PrismML-Eng/llama.cpp](https://github.com/PrismML-Eng/llama.cpp) fork, structured and packaged as drop-in backend extensions for LM Studio on Windows.

---

## Overview

PrismML's Bonsai models utilize custom ternary quantization kernels that are not supported by the default `llama.cpp` builds bundled with LM Studio. Attempting to run Bonsai ternary GGUF files in stock LM Studio will result in load failures or fallback errors.

Building the custom runtime from source with appropriate CUDA dependencies can be complex and time-consuming. This repository provides ready-to-use release builds configured specifically to work inside LM Studio's backend extension system.

---

## Requirements

* Windows 10/11 (64-bit)
* NVIDIA GPU with supported CUDA drivers installed
* [LM Studio](https://lmstudio.ai/) installed

---

## Installation

### 1. Download the Release

Go to the [Releases](../../releases) section of this repository and download the latest `.zip` archive matching your CUDA setup.

The archive will contain a top-level directory named according to the build version and CUDA configuration, structured similar to:

```text
llama.cpp-prism-b<build>-<hash>-bin-win-cuda-<version>-x64-lm-studio
```

*(For example: `llama.cpp-prism-b10709-9a9394a-bin-win-cuda-13.3-x64-lm-studio` or newer builds depending on release).*

---

### 2. Copy to LM Studio Extensions

1. Extract the downloaded `.zip` file.
2. Locate the extracted backend folder (the folder containing the binaries and configuration files).
3. Copy this entire folder directly into LM Studio's backends directory:

```text
C:\Users\<Username>\.lmstudio\extensions\backends\
```

*Quick access tip: You can press `Win + R`, paste the following path, and hit Enter:*

```text
%USERPROFILE%\.lmstudio\extensions\backends
```

After pasting, your directory tree should look similar to:

```text
C:\Users\<Username>\.lmstudio\extensions\backends\
└── llama.cpp-prism-<build-info>-bin-win-cuda-<version>-x64-lm-studio\
    ├── ... (binaries and runtime files)
```

---

### 3. Select the Runtime in LM Studio

1. Open (or restart) **LM Studio**.
2. Open **Settings** (gear icon).
3. Navigate to the **Runtime** section.
4. Under the **GGUF** runtime selector, choose the PrismML backend. It will appear with a name similar to:
   ```text
   Prism ML Cuda xx.x llama.cpp (Windows)
   ```
5. You can now load and run PrismML Bonsai ternary models directly in LM Studio.

---

## Notes & Troubleshooting

* **Backend not appearing in LM Studio:** If the backend does not show up in the settings list, completely exit LM Studio and start it again. Also confirm that you pasted the inner folder itself into `...\extensions\backends\`, not nested folders or just loose files.
* **CUDA Driver Compatibility:** Ensure your installed NVIDIA GPU driver supports the CUDA version indicated in the release build name.
* **Updates:** Whenever a new version is released here, simply repeat the process and remove old backend folders from `.lmstudio\extensions\backends\` if you no longer need them.

---

## Credits & Upstream

* Upstream PrismML fork: [PrismML-Eng/llama.cpp](https://github.com/PrismML-Eng/llama.cpp)
* Base runtime: [ggml-org/llama.cpp](https://github.com/ggml-org/llama.cpp)
* Application: [LM Studio](https://lmstudio.ai/)

Licensed under the MIT License. See [LICENSE](LICENSE) for details.
