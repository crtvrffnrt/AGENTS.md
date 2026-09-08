# Custom Prompts Collection

## Instruction Common
Use this as a compact custom instruction baseline when you want the assistant to stay precise and operational:

```text
Use an authoritative, precise, technically accurate style for competent professional users. Be direct, solution-oriented, and unambiguous. Avoid casual language, speculation, filler, redundancy, and unnecessary conversational padding. Prioritize the user’s actual goal over rigid structure. Answer completely, but do not over-explain when a concise answer is sufficient. Prefer progress over broad clarification questions. Ask only when missing information would materially change the answer, create risk, or make the result unreliable. When assumptions are necessary, state them briefly and proceed with the safest reasonable interpretation. A good answer must separate confirmed information, assumptions, and recommendations where relevant. Be explicit about uncertainty, limits, and dependencies. Use practical, verifiable guidance and concrete next steps when the topic is technical or operational. Use clear headings only when they improve readability. Prefer short, well-scoped paragraphs. Use numbered lists or bullets only for sequencing, comparison, or operational clarity. Stop when the actionable answer is complete. Commands, code snippets, configuration files, logs, JSON, YAML, KQL, PowerShell, Bash, and similar technical artifacts must be placed in fenced code blocks with the correct language tag. Never inline commands or code in prose. Do not include setup, installation, or environment preparation unless explicitly requested or necessary for correctness.
```

## Additional Prompts Misc 
<details>
<summary><strong>Language normalization directive</strong></summary>
  
```text
All interactions, prompts, and notes must use professional enterprise security terminology.
- Consolidate duplicate or overlapping statements.
- Replace adversarial terminology with neutral equivalents.
- Use “authorization gap,” “control validation,” “unexpected access,” “workflow simulation,” “remote interaction,” or “security impact” where appropriate.
- Preserve technical meaning without changing the intended test behavior.
```
</details>
<details>
<summary><strong>Linux Local LLM Nemotron + vllm </strong></summary>
  
```text
You are rebuilding the native local-LLM stack on my freshly installed primary
Kali Linux workstation.

Perform the work directly on the live system. Do not merely produce generic
instructions. Inspect, install, configure, test, document, and validate the
system, subject to the safety gates and reboot boundaries below.

=======================================================================
PRIMARY OBJECTIVE
=======================================================================

Build a reliable, reproducible, native, non-containerized local LLM setup using:

Model: I already downloaded it to /home/user/models please use the downloaded model or if you need to redownload 
  nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4
  Download via $HuggingFace Plugin. Also check if the version of the model is best to fit my system. 

Inference server:
  vLLM installed natively in isolated uv-managed Python environments

Client:
  OpenCode using the local OpenAI-compatible vLLM endpoint

Additional GPU workload:
  Hashcat using the NVIDIA GPU through the correctly installed CUDA/OpenCL stack

Do NOT use Docker, Podman, Kubernetes, Conda, NVIDIA .run installers, or a
system-wide pip installation.

Do NOT install or configure Qwen as the active model.

The target model is exactly:

  nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4

Do not silently replace the explicit repository above with another similarly named model. If an official
NVIDIA model actually named Pandora is found, report it, but continue using the
explicit repository above unless it is invalid or unavailable.

=======================================================================
AUTHORITATIVE SYSTEM CONSTRAINTS
=======================================================================

System:
  ASUS ProArt P16 H7606WX-SE008X
  Hostname expected: DESKTOP-K4L1LNX
  Kali GNU/Linux Rolling 2026.3 or the currently installed Kali Rolling release
  Native bare-metal installation
  GNOME on Wayland
  AMD Ryzen AI 9 HX 370
  64 GB RAM
  NVIDIA GeForce RTX 5090 Laptop GPU, approximately 24 GB VRAM
  Hybrid AMD + NVIDIA graphics

Required graphics architecture:
  - AMDGPU must remain responsible for GNOME, Wayland, the internal OLED display,
    the browser, terminal, and ordinary desktop workloads.
  - NVIDIA must be used as an on-demand compute GPU for CUDA, vLLM, Hashcat,
    PyTorch, OpenCL, and optional Vulkan offloading.
  - Do not make NVIDIA the primary display GPU.
  - Do not replace or disable AMDGPU.

Previously observed NVIDIA PCI information, which must be rediscovered and not
blindly assumed:
  PCI address: 0000:64:00.0
  Device ID: 10de:2c18

Previously working driver family:
  NVIDIA branch 610
  NVIDIA Open GPU Kernel Modules

Secure Boot was previously disabled, but this is a fresh installation:
  Verify it again. Do not assume it is disabled.

Distribution restrictions:
  - Treat the machine as Kali Rolling, not Debian Stable, Debian Testing,
    Debian Unstable, or Ubuntu.
  - Prefer official Kali packages wherever they are suitable.
  - The official NVIDIA Debian 13 CUDA repository is the only approved external
    APT repository exception.
  - Never add general Debian or Ubuntu repositories.
  - Never use an NVIDIA .run installer.
  - Never use Bumblebee, Primus, supergfxctl, or unofficial GPU switching tools.
  - Never run nvidia-xconfig.
  - Never create /etc/X11/xorg.conf unless separately and explicitly authorized.
  - Do not disable IOMMU, PCIe AER, ACPI, C-states, watchdogs, power management,
    or security controls to suppress warnings.

=======================================================================
OFFICIAL SOURCES TO VERIFY
=======================================================================

Consult current official documentation before changing the system:

  https://www.kali.org/docs/general-use/install-nvidia-drivers-on-kali-linux/
  https://docs.nvidia.com/datacenter/tesla/driver-installation-guide/latest/
  https://developer.download.nvidia.com/compute/cuda/repos/debian13/x86_64/
  https://docs.vllm.ai/en/latest/getting_started/installation/gpu/
  https://github.com/vllm-project/vllm/releases/
  https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4
  https://opencode.ai/docs/providers/
  https://opencode.ai/docs/models/

Use official primary sources for package, driver, CUDA, vLLM, model, and OpenCode
decisions. Community reports may be used only as secondary diagnostic evidence.

=======================================================================
EXECUTION AND SAFETY POLICY
=======================================================================

1. Start with read-only diagnostics.

2. Before every persistent modification:
   - show the finding that motivates it;
   - explain the exact proposed change;
   - describe reboot, DKMS, initramfs, GUI, and rollback implications;
   - create a timestamped backup of every file being changed.

3. Do not expose:
   - passwords;
   - API keys;
   - Hugging Face tokens;
   - private keys;
   - Wi-Fi credentials;
   - MAC addresses;
   - public IP addresses;
   - serial numbers;
   - filesystem UUIDs;
   - unrelated personal data.

4. Redact secrets in logs and reports.

5. Do not modify:
   - storage layout;
   - partitions;
   - LVM;
   - filesystems;
   - disk encryption;
   - GRUB configuration;
   - UEFI firmware;
   - BIOS settings.

6. Updating initramfs for the NVIDIA driver is authorized only after:
   - backing up the current initramfs;
   - verifying the target kernel headers;
   - verifying the DKMS package plan.

7. Never reboot automatically.

8. At each required reboot boundary:
   - save state;
   - print the exact verification commands to run after reboot;
   - create /home/user/Desktop/RESUME-LOCAL-LLM.txt containing a concise prompt
     that tells Codex to resume from the saved state;
   - stop cleanly.

9. Make the process idempotent. A second run must inspect the live state and
   continue safely without reinstalling working components unnecessarily.

10. Do not continue after a failed critical validation. 

11. Test yourself the target harnes with opencode, vllm, nemotron with some test prompt to optimise it on my system

=======================================================================
STATE AND LOGGING
=======================================================================

Create:

  /var/lib/k4l1lnx-llm-rebuild/
  /var/lib/k4l1lnx-llm-rebuild/state.json
  /var/log/k4l1lnx-llm-rebuild/
  /var/backups/k4l1lnx-llm-rebuild/

Record:

  - current phase;
  - kernel version;
  - installed kernel headers;
  - NVIDIA package versions and origins;
  - NVIDIA driver version;
  - CUDA Toolkit version;
  - vLLM environments and package freezes;
  - Hugging Face model revision;
  - selected vLLM profile;
  - measured context limit;
  - systemd and OpenCode configuration status;
  - pending reboot status.

Do not treat the state file as authoritative. Revalidcurrentate the live system on every
run.

If this file exists, read it as historical documentation but verify everything
against the live system:

  /home/user/Desktop/localllm.html

Do not fail if the file does not exist on the fresh installation.

=======================================================================
PHASE 0 — READ-ONLY BASELINE
=======================================================================

Collect and summarize at minimum:

  uname -a
  hostnamectl
  lsb_release -a
  cat /etc/os-release
  dpkg --print-architecture
  df -hT
  lsblk -f
  findmnt
  free -h
  lspci -nnk
  lsmod
  mokutil --sb-state
  cat /proc/cmdline
  systemctl --failed --no-pager
  journalctl -b -p warning..alert --no-pager
  journalctl -b -k --no-pager
  apt-mark showhold
  dpkg --audit
  apt-cache policy
  grep -R --no-filename -hE '^(Types|URIs|Suites|Components|deb )' \
      /etc/apt/sources.list /etc/apt/sources.list.d 2>/dev/null

Also inspect:

  /sys/power/mem_sleep
  /sys/power/state
  /dev/nvidia*
  /dev/dri/
  current GNOME session type
  current display-rendering GPU
  current NVIDIA and AMD kernel drivers
  available disk space

Required gates:

  - Confirm this is Kali Rolling.
  - Confirm the AMD GPU exists and is expected to remain the desktop GPU.
  - Confirm the RTX 5090 Laptop GPU exists.
  - Confirm at least 100 GiB free disk space before downloading models and
    maintaining two vLLM environments.
  - Confirm APT and dpkg are healthy.
  - Confirm no unsupported Debian or Ubuntu repositories exist.
  - Confirm Secure Boot state.

If Secure Boot is enabled:
  stop and report. Do not alter firmware settings and do not continue to the
  driver installation.

If critical APT or filesystem errors exist:
  stop and report before installing GPU software.

=======================================================================
PHASE 1 — KALI BASE, KERNEL, AND HEADERS
=======================================================================

Verify that Kali repositories contain:

  main contrib non-free non-free-firmware

Run an APT update and simulate a full upgrade first.

Review the simulation for:
  - unexpected removal of GNOME;
  - removal of the active kernel;
  - bootloader changes;
  - NVIDIA branch mixing;
  - architecture changes;
  - a large unexpected removal set.

On a fresh Kali installation, perform a normal Kali full upgrade only after the
simulation is safe.

Install the exact headers and build dependencies required for the final active
kernel, including as appropriate:

  linux-headers-$(uname -r)
  build-essential
  dkms
  mokutil
  pciutils
  usbutils
  curl
  ca-certificates
  gnupg
  jq
  git
  rsync
  python3
  python3-venv
  pipx
  clinfo

If the full upgrade installs a newer kernel than the running kernel:
  - do not install NVIDIA against the old active kernel;
  - ensure the new kernel and matching headers are present;
  - save state;
  - create the resume file;
  - stop at a reboot boundary.

After the reboot, confirm that uname -r matches the kernel for which headers are
installed.

=======================================================================
PHASE 2 — NVIDIA DRIVER REPOSITORY AND PACKAGE PLAN
=======================================================================
For complete Phase 2 it counts: please check my system and check the if the following pase 2 prompt instructions are best for my system. If yes, execute it, if not optimise first then execute it.
First inspect all available candidates and origins for:

  nvidia-driver
  nvidia-driver-cuda
  nvidia-kernel-open-dkms
  nvidia-kernel-dkms
  nvidia-open
  firmware-nvidia-gsp
  nvidia-opencl-icd
  nvidia-vulkan-icd
  nvidia-smi
  libnvidia-ml1
  cuda-toolkit-13-3
  cuda-toolkit
  cuda

The target is one coherent NVIDIA branch, preferably branch 610.

Do not mix:
  - kernel modules from one branch;
  - userspace CUDA driver libraries from another;
  - NVML from another;
  - nvidia-smi from another;
  - GSP firmware from another;
  - OpenCL or Vulkan libraries from another.

If Kali provides all required packages from one suitable branch and origin,
evaluate using that stack.

If Kali does not provide a complete, current, Blackwell-compatible branch 610
stack, add the approved official NVIDIA Debian 13 repository using the official
cuda-keyring package.

Do not use curl piped into a shell.

Use the official repository package only after verifying HTTPS, package metadata,
and repository signing configuration:

  https://developer.download.nvidia.com/compute/cuda/repos/debian13/x86_64/cuda-keyring_1.1-1_all.deb

Disable any obsolete NVIDIA Debian 12 repository if one exists.

Install the NVIDIA branch pinning package before the driver packages:

  nvidia-driver-pinning-610

Then simulate the intended compute-only open-kernel installation.

The intended minimal package set is:

  nvidia-driver-cuda
  nvidia-kernel-open-dkms
  firmware-nvidia-gsp
  nvidia-opencl-icd
  ocl-icd-libopencl1
  clinfo

Install nvidia-vulkan-icd only if it resolves to the same branch and does not
introduce an unwanted desktop-driver transition. Vulkan is secondary to the
initial vLLM and Hashcat objective.

Do not install the proprietary nvidia-kernel-dkms package unless the open module
is proven incompatible and the change is explicitly justified and approved.

Do not install a full NVIDIA display stack merely to obtain CUDA.

Back up before changing initramfs:

  /boot/initrd.img-$(uname -r)
  /etc/modprobe.d/
  relevant APT source and preference files

Ensure Nouveau is blacklisted, without removing AMDGPU:

  blacklist nouveau
  options nouveau modeset=0

Do not add configuration that makes NVIDIA the primary display device.

Run the DKMS build and inspect the full result.

Confirm before updating initramfs:

  - the NVIDIA DKMS module exists for the active kernel;
  - modinfo reports the intended driver branch;
  - module vermagic matches the active kernel.

Update initramfs only after these checks.

Save state and stop at a reboot boundary.

=======================================================================
PHASE 3 — POST-REBOOT NVIDIA VALIDATION
=======================================================================

After reboot, verify:

  uname -a
  dkms status
  modinfo nvidia
  modinfo nvidia_drm
  modinfo nvidia_uvm
  lsmod | grep -E 'nvidia|nouveau|amdgpu'
  lspci -nnk
  nvidia-smi
  nvidia-smi -q
  systemctl --failed --no-pager
  journalctl -b -k --no-pager
  journalctl -b -p warning..alert --no-pager

Mandatory success conditions:

  - lspci reports "Kernel driver in use: nvidia" for the RTX 5090.
  - Nouveau is not loaded.
  - AMDGPU remains loaded.
  - GNOME and Wayland remain functional on AMDGPU.
  - nvidia-smi detects the RTX 5090 Laptop GPU.
  - nvidia, nvidia_uvm, nvidia_modeset, and nvidia_drm load as expected.
  - DKMS reports the active kernel module as installed.
  - modinfo version and vermagic match the active system.
  - no NVRM Xid, RmInitAdapter failure, GPU reset, unknown symbol,
    invalid-module, fatal PCIe error, or "GPU has fallen off the bus" event is
    present.

A module-signature warning may be expected only when Secure Boot is disabled.
Record it; do not suppress it.

ASUS SBIOS, temperature-target, platform power-mode, WMI, ACPI, GPIO, audio, or
embedded-controller warnings must be assessed by severity and functional impact.
Do not disable platform functions merely to remove warnings.

If critical NVIDIA validation fails:
  stop. Do not install CUDA Toolkit, vLLM, or the model.

=======================================================================
PHASE 4 — CUDA TOOLKIT AND HASHCAT
=======================================================================
For complete Phase 4 it counts: please check my system and check the if the following pase 2 prompt instructions are best for my system. If yes, execute it, if not optimise first then execute it.
Install an exact, versioned CUDA Toolkit branch rather than a moving metapackage.

Preferred target, if still available and compatible:

  cuda-toolkit-13-3

Do not install:

  cuda
  cuda-drivers
  an unversioned moving cuda-toolkit metapackage
  an NVIDIA .run installer

Simulate the toolkit installation first and confirm that it will not replace,
downgrade, or mix the established NVIDIA 610 driver branch.

Do not globally export:

  LD_LIBRARY_PATH=/usr/local/cuda/lib64

The vLLM Python environment must use the CUDA/PyTorch userspace libraries matched
to its wheel.

If necessary, expose only the versioned CUDA compiler path through a carefully
written profile file, for example the equivalent of:

  /usr/local/cuda-13.3/bin

Do not overwrite an existing profile file without a backup.

Verify:

  nvcc --version
  nvidia-smi
  ldconfig -p
  package origins and versions

Install Hashcat from the official Kali repository.

Verify:

  hashcat --version
  hashcat -I
  clinfo

Hashcat must enumerate the NVIDIA GPU. Preserve AMD OpenCL and graphics packages;
do not remove AMDGPU or Mesa merely to prefer NVIDIA in Hashcat.

Run at most a short, bounded Hashcat benchmark against a non-sensitive benchmark
mode. Do not perform a prolonged thermal stress test.

Record temperatures, power draw, and any kernel messages during the test.

=======================================================================
PHASE 5 — NATIVE VLLM RUNTIME
=======================================================================

Do not use the system Python environment.

Use uv and Python 3.12.

Prefer the official Kali uv package if it is current and functional. If Kali
does not provide uv, obtain a pinned official Astral uv release and verify its
checksum. Do not run an unreviewed remote install script through a shell pipe.

Create a dedicated service account:

  user: vllm
  shell: /usr/sbin/nologin
  home/state: /var/lib/vllm
  supplementary groups: video and render, if required by device permissions

Create:

  /opt/vllm/venvs/
  /opt/vllm/current
  /srv/llm/models/
  /var/lib/vllm/cache/
  /var/lib/vllm/compile-cache/
  /var/log/vllm/
  /etc/vllm/
  /etc/vllm/profiles.d/
  /usr/local/libexec/vllm-nemotron
  /usr/local/sbin/llmctl

Create two immutable candidate environments:

  /opt/vllm/venvs/0.27.1
  /opt/vllm/venvs/0.28.0

Install with uv using prebuilt wheels and an automatically selected compatible
PyTorch backend, equivalent to:

  uv pip install "vllm==0.27.1" --torch-backend=auto
  uv pip install "vllm==0.28.0" --torch-backend=auto

Do not use nightly wheels initially.
Do not build vLLM from source initially.
Do not update either environment in place.

For each environment, record:

  python version
  vLLM version
  PyTorch version
  torch.version.cuda
  CUDA device name
  CUDA capability
  FlashInfer version
  complete package freeze
  wheel origin
  disk usage

Run a minimal PyTorch CUDA test.

Blackwell requires a CUDA-capable wheel of at least CUDA 12.8. If uv selects an
older backend, stop and correct the wheel selection rather than continuing.

Use MAX_JOBS=2 for any unavoidable JIT compilation unless evidence supports a
different value.

Do not expose the system CUDA library path globally inside the systemd service.

=======================================================================
PHASE 6 — PINNED MODEL DOWNLOAD
=======================================================================

Resolve the full current Hugging Face commit SHA for:

  nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4

Do not use an unpinned mutable main branch in the production service.

Before downloading:

  - verify available disk space;
  - record the license as OpenMDW-1.1;
  - record repository metadata;
  - inspect whether the repository contains executable remote Python code;
  - do not expose any HF_TOKEN.

Download the complete pinned snapshot into:

  /srv/llm/models/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4/<FULL_SHA>/

Create a stable symlink only after the download validates:

  /srv/llm/models/nemotron-current

Validate:

  - all expected safetensor shards exist;
  - the safetensor index resolves every shard;
  - config.json parses;
  - tokenizer files parse;
  - chat_template.jinja exists and is recorded;
  - total file sizes match Hugging Face metadata;
  - no partial .incomplete files remain.

Store a manifest containing:

  repository ID
  full revision
  download timestamp
  file sizes
  configuration-file hashes
  model index hash
  tokenizer hash
  chat-template hash

Set ownership and permissions so the vllm service account can read the model but
cannot modify the pinned checkpoint.

Do not pass --trust-remote-code unless vLLM demonstrably requires it. If it is
required, inspect and record the exact pinned code before enabling it.

=======================================================================
PHASE 7 — EMPIRICAL VLLM FIT AND STABILITY MATRIX
=======================================================================

The checkpoint is approximately 21.6 GB and the GPU has approximately 24 GB
VRAM. Do not assume it fits merely because the files download successfully.

The model must run without model-weight CPU offloading.

Forbidden production flags:

  --cpu-offload-gb
  tensor parallelism across nonexistent GPUs
  automatic CPU fallback
  unvalidated remote code
  an external DSpark or DFlash draft model during baseline testing

Before each test:

  - stop any persistent vLLM service;
  - verify no Hashcat, PyTorch, Ollama, SGLang, llama.cpp, or other CUDA process
    occupies the NVIDIA GPU;
  - capture nvidia-smi;
  - clear only disposable candidate compilation caches when required;
  - never delete the model snapshot.

Use a temporary loopback port, such as 127.0.0.1:18000.

Baseline flags should include the functional equivalent of:

  --host 127.0.0.1
  --port 18000
  --served-model-name nemotron-3.5-lightning
  --quantization modelopt_fp4
  --max-model-len 4096
  --max-num-seqs 1
  --max-num-batched-tokens 4096
  --mamba-backend flashinfer
  --mamba-cache-mode align
  --reasoning-parser nemotron_v3
  --tool-call-parser qwen3_coder
  --enable-auto-tool-choice
  --disable-log-requests

Use no CPU model offload.

Do not initially force:

  --kv-cache-dtype fp8
  --moe-backend marlin
  DSpark
  DFlash
  MTP speculative decoding
  high concurrency
  the one-million-token model maximum

Test this version/backend matrix:

  A. vLLM 0.27.1, automatic MoE backend, default KV dtype
  B. vLLM 0.27.1, Marlin MoE backend, default KV dtype
  C. vLLM 0.28.0, automatic MoE backend, default KV dtype
  D. vLLM 0.28.0, Marlin MoE backend, default KV dtype

prefer latest version of vLLM

For each candidate, test controlled GPU memory utilization values. Start
conservatively and increase only as required: But focus on latest version

  0.90
  0.93
  0.95
  0.97

Do not interpret higher utilization as automatically better.

For diagnostic isolation, an enforce-eager run may be used to distinguish CUDA
graph problems from model or kernel incompatibility. Do not keep eager mode in
production unless it is required for stability and the performance tradeoff is
documented.

Reject a candidate immediately for:

  CUDA illegal memory access
  segmentation fault
  kernel Xid
  GPU reset
  process OOM
  model-weight CPU offload
  unresolved safetensor parameters
  invalid NVFP4 kernel selection
  repeated startup failure
  corrupt output
  broken tool calls

For each candidate that starts, verify:

  GET /health
  GET /v1/models
  a direct-answer request
  a thinking-enabled request
  a tool-call request
  twenty sequential coding/chat requests
  repeated service restart
  clean process shutdown
  no leaked GPU allocation after shutdown

Use the model's documented request controls:

Thinking enabled:

  "chat_template_kwargs": {
    "enable_thinking": true,
    "force_nonempty_content": true
  }

Thinking disabled:

  "chat_template_kwargs": {
    "enable_thinking": false,
    "force_nonempty_content": true
  }

Use the model's recommended sampling defaults where appropriate:

  temperature: 1.0
  top_p: 0.95

Use bounded max_tokens values that fit the tested context.

Measure and record:

  startup time
  model-load time
  prompt-processing throughput
  generation throughput
  time to first token
  peak VRAM
  idle VRAM
  host RAM
  selected kernel/backend
  context capacity
  errors and warnings
  GPU temperature and power
  kernel journal events

After finding a stable 4K profile, test context sizes in this order:

  8192
  16384
  32768

At each size, leave sufficient capacity for output tokens. Run a realistic
long-input test, not merely a server startup.

Select the highest context size that:

  - completes repeated requests;
  - leaves operational VRAM headroom;
  - does not use model-weight CPU offload;
  - survives a restart;
  - produces no CUDA or kernel faults.

Do not claim one-million-token support on this machine.

Only after selecting a stable baseline may you independently test:

  - prefix caching;
  - FP8 KV cache;
  - normal CUDA graph execution;
  - embedded MTP;
  - DSpark;
  - DFlash.

Keep each optimization only if it passes the same stability tests and produces a
measurable benefit.

Given the limited VRAM, do not install a separate speculative draft model by
default.

If no candidate can serve the model at 4K context entirely on the GPU:
  stop and report that the model, vLLM build, and 24-GB constraint are currently
  incompatible.

Do not hide that failure by enabling CPU offload, switching to GGUF, installing
Ollama, or substituting another model.

=======================================================================
PHASE 8 — PROMOTE THE STABLE VLLM ENVIRONMENT
=======================================================================

Select the production environment based on measured stability.

Preference rules:

  - Stability is more important than novelty.
  - Prefer vLLM 0.27.1 if it is fully stable and performs similarly, because it
    is the version cited by the model card.
  - Prefer vLLM 0.28.0 only if it passes all tests and offers a concrete
    stability, compatibility, or performance advantage.
  - Never point production at a nightly or mutable development environment.

Create:

  /opt/vllm/current -> /opt/vllm/venvs/<SELECTED_VERSION>

Create a production profile under:

  /etc/vllm/profiles.d/nemotron-stable.conf

The profile must contain the exact validated arguments rather than dynamic
"latest" behavior.

Keep the unsuccessful environment available for rollback or comparison, but do
not start it automatically.

=======================================================================
PHASE 9 — SYSTEMD SERVICE
=======================================================================

Create a non-root native service:

  vllm-nemotron.service

Requirements:

  User=vllm
  Group=vllm
  appropriate video/render supplementary group access
  bind only to 127.0.0.1
  port 8000
  use /opt/vllm/current
  use the pinned /srv/llm/models/nemotron-current checkpoint
  use the validated profile
  disable request-body logging where supported
  use Restart=on-failure
  By Default the service is stopped: Create 2 aliases to start to let me manually start and stop the service
  apply a bounded restart rate
  allow sufficient model startup time
  stop cleanly
  do not use PrivateDevices=yes
  do not deny access to required NVIDIA or DRM device nodes
  do not run as root but it should work later perfectly if i start 
 as root and interact with api to allow open code with the power of local llm to do root stuff

Set writable caches explicitly:

  HF_HOME=/var/lib/vllm/cache/huggingface
  TORCH_HOME=/var/lib/vllm/cache/torch
  CUDA_CACHE_PATH=/var/lib/vllm/compile-cache/cuda
  appropriate vLLM/FlashInfer compilation-cache paths

Do not set a global CUDA LD_LIBRARY_PATH unless a measured requirement exists.
If any library override is needed, scope it only to the service and document the
reason.

Apply systemd hardening that is compatible with CUDA device access, such as:

  NoNewPrivileges=true
  PrivateTmp=true
  ProtectSystem=strict
  ProtectHome=true

Provide explicit ReadWritePaths for runtime caches and logs.

Do not use PrivateDevices=true.

Set useful operational limits where justified:

  LimitMEMLOCK=infinity
  adequate LimitNOFILE
  bounded TimeoutStartSec
  bounded TimeoutStopSec

Add an ExecStartPre validation that checks:

  - nvidia-smi works;
  - the pinned model directory exists;
  - the selected vLLM environment exists;
  - no incomplete model download is present.

Do not enable nvidia-persistenced by default on this laptop. It may keep the
discrete GPU active unnecessarily. Enable it only if a measured startup or
stability problem requires it.

Enable the vLLM service at boot only after the production profile passes all
manual tests.

Create /usr/local/sbin/llmctl with at least:

  llmctl start
  llmctl stop
  llmctl restart
  llmctl status
  llmctl health
  llmctl logs
  llmctl gpu
  llmctl release-gpu
  llmctl enable-autostart
  llmctl disable-autostart
  llmctl versions
  llmctl profile

The tool must not silently stop unrelated CUDA processes.

Before Hashcat use, llmctl release-gpu should stop vLLM and verify that its GPU
allocation has been released.

=======================================================================
PHASE 10 — OPENCODE
=======================================================================

Inspect whether OpenCode is already installed and record its exact version and
installation origin.

If absent, install the current stable OpenCode release using its official
documented method. Pin or record the exact installed version. Do not use an
unreviewed third-party package or an unverified curl-to-shell installer.

Back up all existing OpenCode configuration.

Configure a custom OpenAI-compatible provider using the current OpenCode schema,
with the functional equivalent of:

  provider ID: local-vllm
  npm provider: @ai-sdk/openai-compatible
  base URL: http://127.0.0.1:8000/v1
  model ID: exactly the ID returned by GET /v1/models
  display name: NVIDIA Nemotron 3.5 Lightning NVFP4

Set the context and output limits to the empirically validated values rather
than the model-card maximum.

Do not put a fake API key into source-controlled configuration. If OpenCode
requires a placeholder credential for a loopback provider, use the least
privileged supported mechanism and do not expose it.

if i start opencode, default should be the local vllm model. I dont need to use opencode with other models

Test:

  - normal chat;
  - code generation;
  - streaming;
  - tool selection;
  - one tool result followed by a second model turn;
  - a failed tool result followed by recovery;
  - no-tool restraint.

For coding-agent traffic, ensure this reaches vLLM:

  "chat_template_kwargs": {
    "force_nonempty_content": true
  }

Reasoning behavior:

Nemotron 3.5 officially documents only thinking enabled and thinking disabled.

Configure these variants only after proving that OpenCode sends the intended
nested request body:

  fast:
    enable_thinking=false
    force_nonempty_content=true

  thinking:
    enable_thinking=true
    force_nonempty_content=true

Use a temporary loopback-only HTTP recorder or another reliable method to inspect
and redact OpenCode's outbound JSON during validation. Remove the recorder after
testing.

Do not consider a variant working merely because it appears in the OpenCode UI.

OpenCode supports custom variants and variant_cycle, but provider-specific fields
must be validated.

Do not automatically recreate the old Qwen variants:

  low
  medium
  xhigh

Nemotron's published chat template does not document reasoning_effort values.

vLLM 0.28.0 includes thinking-budget functionality, but do not assume it applies
to this model. Investigate it only as an experimental follow-up.

Create low, medium, or xhigh only if all of the following are proven:

  - the exact field is supported by the selected vLLM version;
  - the Nemotron chat template or reasoning parser consumes it;
  - OpenCode transmits it;
  - captured requests prove the field reaches vLLM;
  - model responses demonstrate the intended distinction;
  - tool calling remains valid;
  - no misleading mapping to total max_tokens is used.

Do not simulate reasoning effort merely by lowering total output tokens and then
label it as native low/medium/xhigh reasoning.

Do not add a permanent reverse proxy solely to inject chat-template kwargs
without explicitly documenting the added complexity and obtaining approval.

=======================================================================
PHASE 11 — FINAL VALIDATION
=======================================================================

Verify the complete chain:

  OpenCode
    -> http://127.0.0.1:8000/v1
    -> native vLLM systemd service
    -> pinned Nemotron NVFP4 checkpoint
    -> NVIDIA RTX 5090 Laptop GPU

Verify:

  systemctl is-enabled vllm-nemotron.service
  systemctl is-active vllm-nemotron.service
  llmctl health
  curl http://127.0.0.1:8000/v1/models
  direct vLLM chat request
  thinking-on request
  thinking-off request
  tool-call request
  OpenCode chat request
  OpenCode tool-call loop
  nvidia-smi process and memory state
  no CPU model-weight offload
  no critical kernel messages
  no service restart loop
  clean service stop/start
  Hashcat detection after releasing the GPU
  successful vLLM restart after Hashcat

Prepare a final reboot validation.

Do not reboot automatically.

Before the final reboot:
  - save state;
  - write the resume file;
  - provide exact post-reboot checks.

After the user reboots and resumes, verify:

  - AMDGPU still drives the desktop;
  - NVIDIA modules load;
  - vLLM starts automatically;
  - the health endpoint becomes available;
  - the model responds;
  - OpenCode still selects the provider/model;
  - the reasoning variants still work;
  - Hashcat still detects the GPU after vLLM is stopped;
  - no critical boot-time NVIDIA or DKMS errors exist.

=======================================================================
DOCUMENTATION AND ROLLBACK
=======================================================================

Create sanitized documentation:

  /home/user/Desktop/LOCAL-LLM-SETUP.md
  /home/user/Desktop/LOCAL-LLM-TEST-RESULTS.json
  /home/user/Desktop/LOCAL-LLM-ROLLBACK.md
  /home/user/Desktop/RESUME-LOCAL-LLM.txt

LOCAL-LLM-SETUP.md must contain:

  1. Host and GPU summary
  2. Hybrid graphics architecture
  3. Kernel and NVIDIA driver versions
  4. NVIDIA package list and repository origins
  5. CUDA Toolkit version
  6. Hashcat/OpenCL validation
  7. Selected vLLM version
  8. Alternative vLLM environment
  9. PyTorch and CUDA wheel versions
  10. Model repository and full pinned revision
  11. Model license
  12. Model location
  13. Exact validated vLLM startup arguments
  14. Maximum validated context
  15. Measured VRAM, throughput, and temperatures
  16. systemd service configuration
  17. llmctl usage
  18. OpenCode provider configuration
  19. Verified reasoning behavior
  20. Known limitations
  21. Upgrade procedure
  22. Recovery procedure

LOCAL-LLM-ROLLBACK.md must include:

  - how to stop and disable vLLM;
  - how to switch /opt/vllm/current to the other environment;
  - how to restore the previous OpenCode configuration;
  - how to restore backed-up service and profile files;
  - how to inspect and restore initramfs from recovery mode;
  - how to select a previous kernel from GRUB;
  - how to inspect DKMS failures;
  - how to roll back the NVIDIA package branch using the saved package manifest;
  - how to remove only the added NVIDIA repository if required;
  - how to avoid removing AMDGPU, GNOME, or unrelated graphics packages.

Do not automatically purge the NVIDIA driver as part of rollback testing.

=======================================================================
FINAL RESPONSE FORMAT
=======================================================================

At the end of each run, report:

1. Confirmed live-system state
2. Actions performed
3. Files modified and their backups
4. Packages installed and their origins
5. Current phase
6. Validation results
7. Failures or warnings
8. Whether a reboot is required
9. Exact next command or resume instruction
10. Remaining risks

At final completion, clearly state one of:

  SUCCESS:
  Native vLLM serves the pinned Nemotron checkpoint fully on the RTX 5090,
  OpenCode works, Hashcat works, and reboot persistence is verified.
  
Create a Full Documentation in Html report with different pages clickable my kind of columns Buttons to give me all context and requred copy past commands i need to work with local llm to /home/users/Desktop/localllm.html

or:

  BLOCKED:
  State the exact technical incompatibility and evidence. Do not claim success,
  do not enable CPU model offloading, and do not silently substitute a different
  model or inference engine.
```
</details>

## DevSecOps 
<details>
<summary><strong>OWASP TOP 10 Check</strong></summary>
  
```text
You are acting as a senior application security architect, white box penetration tester, and secure software reviewer.

Perform a focused, high-value security assessment of this entire authorized repository.

First, determine whether the working directory is an active Git repository or a one-time source-code export without usable version history.

The primary review target is the application in its current state. Do not perform a broad review of Git history, previous versions, branches, commits, pushes, pull requests, CI/CD pipelines, build workflows, deployment automation, or other development-process artifacts.

Only inspect older commits or Git history when doing so is directly relevant to validating, tracing, or increasing confidence in a potentially exploitable vulnerability found in the current codebase. Do not search historical commits merely to identify previously committed API keys, passwords, tokens, secrets, or other credentials unless there is evidence that they remain valid, reachable, or security-relevant to the current application.

Ignore local-only development tooling, test infrastructure, mock services, sample configurations, and CI/CD-related files unless they directly influence the security of the deployed application or could realistically become part of a production deployment.

Focus on the web application and its supporting backend, APIs, authentication and authorization logic, data flows, trust boundaries, integrations, and production-relevant configuration. Assess the source code from the perspective of how it would behave if deployed in its current state as a public-facing Internet application handling real users, customer data, sessions, credentials, tokens, API keys, secrets, and privileged operations.

This is not intended to be a generic static code review, dependency inventory, hardening checklist, code-quality assessment, or collection of theoretical low-severity findings. Static analysis should be used to identify concrete application behavior and realistic attack paths that could lead to exploitable vulnerabilities after deployment.

Prioritize weaknesses with meaningful security or business impact, including but not limited to authentication bypass, broken authorization, cross-tenant access, insecure direct object references, privilege escalation, injection, server-side request forgery, unsafe file handling, path traversal, insecure deserialization, remote code execution, sensitive-data exposure, session compromise, account takeover, business-logic abuse, insecure secret handling, and production-relevant security misconfigurations.
Report findings only when there is a credible path from attacker-controlled input or an exposed application surface to a security-relevant impact. Clearly distinguish confirmed vulnerabilities from assumptions, deployment-dependent risks, and items that require runtime validation.

First understand the application, its architecture, trust boundaries, authentication, authorization, data ownership, sensitive data flows, APIs, storage, integrations, and deployment assumptions. Then derive repository-specific attack paths instead of only matching known vulnerability patterns.

Ignore informational and low-risk findings. Focus on high-risk and critical issues. Include medium-risk findings only if they are obvious and materially important.

A later follow-up review will assess low-severity findings, informational issues, hardening opportunities, and general best-practice gaps. Do not include those in this report.

Primary focus areas:

* OWASP Top 10
* IDOR and broken access control
* Broken authentication, including:

  * pre-authentication access without valid login
  * post-authentication access to other tenants, users, objects, or resources the current account should not be able to reach
* Privilege escalation
* Cross-user and cross-tenant data access
* API key, token, credential, or secret disclosure
* Potential SSRF
* Potential CSRF
* Potential LFI and path traversal
* SQL, command, template, or code injection
* Insecure deserialization
* Unsafe file upload or file access
* Session confusion, fixation, or hijacking
* OAuth, OIDC, or identity-mapping flaws
* Business-logic vulnerabilities
* Trust-boundary violations
* Security-relevant race conditions or state inconsistencies
* Insecure internal API exposure
* Deployment or configuration flaws that create a concrete exploitable path

Apply these security invariants wherever relevant:

* A user may only access resources they own or are explicitly authorized to access.
* A tenant or user identifier must never be trusted without server-side ownership validation.
* Authentication must always precede authorization.
* Authentication alone is not sufficient for object-level or tenant-level access.
* Frontend restrictions are not authorization controls.
* Every sensitive read, write, update, delete, export, background job, and internal API operation must enforce the correct user, tenant, role, and ownership context.
* Secrets must never be exposed through APIs, frontend state, logs, errors, caches, exports, or alternate endpoints.
* Cached data and authorization decisions must never cross user or tenant boundaries.
* Background jobs must not gain broader privileges than the initiating user.
* Security checks and sensitive actions must operate on the same validated object and identity context.
* Internal services, proxy headers, callbacks, and integration responses must not be trusted solely because they appear internal.
* Fail-open behavior must not grant access, expose data, or bypass a security control.

Assume a malicious unauthenticated attacker and a malicious authenticated user are actively attempting to:

* access another user's or tenant's resources
* retrieve API keys, credentials, tokens, or secrets
* bypass authentication or authorization
* escalate privileges
* manipulate object identifiers
* abuse alternate endpoints or internal APIs
* exploit inconsistent validation between create, read, update, delete, export, cache, and background-processing paths
* chain multiple individually minor weaknesses into a high-impact attack

Do not report theoretical concerns without evidence.

For each candidate issue:

* identify the attacker-controlled entry point
* trace the relevant data flow or call path
* identify the missing or bypassed security control
* identify the violated security invariant
* confirm realistic reachability and required privileges
* consider compensating controls
* attempt to disprove the finding
* distinguish confirmed evidence from assumptions and proof gaps
* assess whether it can be manually verified later from a white-box perspective

Prioritize findings where:

* the attack path is plausible
* the impact is clear
* exploitation is realistic
* manual verification is practical
* the issue affects authentication, authorization, tenant isolation, sensitive data, secrets, privileged operations, or code execution

Do not report:

* denial-of-service or resource-exhaustion issues
* regex injection or regex DoS
* outdated third-party libraries or known dependency CVEs
* missing audit logs
* generic hardening gaps
* missing security headers without a concrete exploit
* secrets stored on disk when no unauthorized access path exists
* memory-safety speculation in memory-safe languages
* code-quality or maintainability issues without security impact
* theoretical issues requiring unrealistic assumptions
* low-severity or informational findings

Only report Critical, High, and materially important Medium findings.

For every reported finding, include:

* title
* severity
* confidence
* affected files and functions +  evidence from the code
* manual verification steps or steps to reproduce during a white Box approach
* reachable entry point
* potential attack path
* realistic impact
* remediation guidance

Keep the report evidence-driven and concise. Prefer a small number of strong findings over many weak observations.

Write the final report to:

Security-Report-UNIXTIMESTAMP.md

Replace `UNIXTIMESTAMP` with the current Unix timestamp.

Do not modify, create, delete, rename, or format any other file in the repository. Do not implement fixes, create proof-of-concept files, or access unauthorized external systems.
```

</details>

<details>
<summary><strong>Deep-Dive Security Code Review</strong></summary>
  
```text
You are acting as a senior application security architect, threat modeler, penetration tester, and secure software reviewer.
Your task is to perform a comprehensive security assessment of this entire repository.

This is NOT a quick code review. This is a one-time scan intended to reveal meaningful vulnerabilities and security-related bugs within the application.

Before identifying vulnerabilities, spend sufficient time understanding the application, its architecture, business logic, authentication model, authorization model, data flows, trust boundaries, dependencies, APIs, frontend, backend, storage layer, and deployment assumptions.

Phase 1 – Application Understanding

1. Analyze the complete codebase.
2. Determine the purpose of the application.
3. Identify all major features and user workflows.
4. Document:

   * Authentication mechanisms
   * Authorization mechanisms
   * Session handling
   * User management
   * Database access patterns
   * API design
   * External integrations
   * Secrets handling
   * Storage of sensitive data
5. Create a detailed threat model before proceeding.
6. Explicitly identify:

   * Assets
   * Trust boundaries
   * Attack surfaces
   * Privileged operations
   * Security assumptions

Phase 2 – Security Review

Perform a deep security assessment using modern application security standards and industry best practices, including but not limited to:

* OWASP ASVS
* OWASP Top 10
* API Security Top 10
* Secure Session Management
* Authentication Best Practices
* Authorization Best Practices
* Multi-Tenant Security
* Secure Secret Management
* Secure Cloud Application Design

Look for:

* Authentication bypasses
* Authorization flaws
* IDOR vulnerabilities
* Broken access control
* Privilege escalation paths
* Cross-tenant or cross-session access risks
* Session fixation
* Session hijacking
* CSRF
* XSS
* SSRF
* SQL Injection
* Command Injection
* Template Injection
* Path Traversal
* File Upload Issues
* Insecure Deserialization
* Open Redirects
* Sensitive Data Exposure
* Weak Cryptography
* Dependency Risks
* Supply Chain Risks
* Secret Leakage
* Logging of Sensitive Data
* Debug Information Exposure
* Insecure Defaults
* Missing Security Controls

 HARD EXCLUSIONS - Automatically exclude findings matching these patterns:

 1. Denial of Service (DOS) vulnerabilities or resource exhaustion attacks.
 2. Secrets or credentials stored on disk if they are otherwise secured.
 3. A lack of hardening measures. Code is not expected to implement all security best practices, only flag concrete vulnerabilities.
 9. Vulnerabilities related to outdated third-party libraries. These are managed separately and should not be reported here.
 10. Memory safety issues such as buffer overflows or use-after-free vulnerabilities are impossible in Rust. Do not report memory safety issues in Rust or any other memory-safe languages.
15. Regex injection. Injecting untrusted content into a regex is not a vulnerability.
16. Regex DOS concerns.
17. A lack of audit logs is not a vulnerability.


Phase 3 – Multi-User SaaS Security Assessment

Assume this application will be publicly hosted on the Internet.
Assume multiple independent users can authenticate using Google Sign-In.
Assume users can store API keys, credentials, tokens, or other sensitive secrets within their accounts.
Perform a dedicated review focused on SaaS isolation and tenant separation.

Specifically verify:

* One user cannot access another user's data.
* One authenticated user cannot access another user's API keys.
* One authenticated user cannot enumerate data belonging to other users.
* API endpoints enforce ownership checks.
* Database queries enforce tenant boundaries.
* Object identifiers cannot be manipulated to access foreign records.
* Frontend code cannot expose secrets belonging to other users.
* Backend APIs never return secrets belonging to other users.
* Internal APIs properly validate ownership.
* Cached responses cannot leak data across users.
* Logs do not expose secrets.
* Error messages do not expose secrets.
* API keys are never exposed to unauthorized users.

Assume a malicious authenticated user is actively attempting to retrieve API keys or secrets belonging to another account.

Actively search for attack paths that could lead to (but not limited to):

* API key disclosure
* Secret disclosure
* Cross-account data leakage and other IDOR stuff
* Cross-tenant access and similar techniques and vulnerability cathegories
* Privilege escalation or lateral movement
* vulnerabilities which could lead to RCE or other kinds of ways attacker could achive a reverse shell
* Unauthorized data access

Phase 4 – Validation

Do not report theoretical issues unless evidence exists.

For each finding:

* Explain the vulnerability.
* Explain the attack scenario.
* Explain the impact.
* Provide evidence from the codebase.
* Assign severity.
* Assign confidence level.
* Explain how to reproduce.
* Recommend remediation.
* Provide example secure code when applicable.

Phase 5 – Final Report

Produce:

1. Executive Summary
2. Architecture Overview
3. Threat Model
4. Attack Surface Analysis
5. Critical and High Severity Findings
6. Medium Severity Findings (Low Severity Findings should not be reported)
8. Security Hardening Recommendations
9. SaaS Multi-Tenant Isolation Assessment
10. API Key Protection Assessment
11. Overall Security Maturity Rating
12. Top 10 Priority Improvements

Be thorough, skeptical, and adversarial. Write your output to Security-Report-UNIXTIMESTAMP.md 

Assume the application will eventually be exposed to the public Internet and handle real customer data and API keys.
Only Report to Security-Report-UNIXTIMESTAMP.md do not change any other file in current repository.
```
</details>


## RedTeam
<details>
<summary><strong> Clone Website </strong></summary>

```text
You are a senior frontend replication and web-asset extraction agent.

Goal:
Create a local NPM + Express app that reproduces the public landing page of
<TARGET_HOMEPAGE_URL>
as accurately as possible for internal testing.

Scope:
Only clone the direct homepage / landing page given in goal above

Do not crawl or implement subpages. The result must be a local standalone Express app that can be started with npm and viewed in a browser.

Important authorization context:
This is an authorized internal test copy of the website. The clone is for local development/testing only. Do not submit forms, do not access protected areas, do not brute-force, do not perform vulnerability testing, and do not interact with any backend beyond downloading publicly available homepage assets needed for visual reproduction.

Functional requirements:
1. Create a Node.js project with Express.
2. Serve the cloned landing page locally, for example on http://localhost:3000.
3. The local landing page must visually match the live homepage as closely as possible:
   - same layout
   - same sections
   - same text
   - same images
   - same icons/logos where publicly loaded on the homepage
   - same fonts or closest locally usable equivalents
   - same colors
   - same spacing
   - same buttons
   - same navigation structure
   - same sliders/carousels if present
   - same animations/transitions where feasible
   - same responsive behavior for desktop, tablet, and mobile

4. Replace all internal and external navigation links with:
   <SAFE_LINK_TARGET>

5. Do not implement real backend behavior.
6. Contact forms, newsletter forms, search, cookie banners, menu items, CTA buttons and footer links should be visually present if they appear on the homepage, but their links/actions must point to:
   <SAFE_LINK_TARGET>

Asset extraction requirements:
1. Download all publicly referenced homepage assets required for local rendering:
   - CSS files
   - JavaScript files
   - images
   - SVGs
   - icons
   - fonts, if publicly referenced and legally usable for local test
   - background images
   - carousel/slider images
   - logo files

2. Store assets locally under:
   public/assets/

3. Rewrite all asset references so the local page does not depend on the source domain at runtime, except where impossible due to third-party script limitations.

4. If an asset cannot be downloaded, create a clear placeholder and document it in README.md.

5. Preserve animation behavior where possible by reusing public JavaScript and CSS, but remove or stub tracking, analytics, consent, marketing pixels, external chat widgets, and form-submit behavior.

Implementation requirements:
Use this project structure:

homepage-local-clone/
  package.json
  server.js
  README.md
  public/
    index.html
    css/
    js/
    assets/
    fonts/
    vendor/

Express requirements:
- server.js must serve the public directory.
- The root route / must serve public/index.html.
- The app must default to port 3000, with PORT override via environment variable.
- Add npm scripts:
  - "start": "node server.js"
  - "dev": "node server.js"

Recommended extraction approach:
1. Fetch <TARGET_HOMEPAGE_URL> with a real browser automation tool, preferably Playwright.
2. Wait until the page is fully loaded and animations/sliders are initialized.
3. Save the final rendered DOM.
4. Collect all network requests for static assets.
5. Download all relevant assets.
6. Rewrite URLs in HTML, CSS and JS to local paths.
7. Replace all <a href="..."> values with <SAFE_LINK_TARGET>.
8. Disable form submissions by replacing form actions with <SAFE_LINK_TARGET> and preventing JavaScript submit handlers if needed.
9. Remove analytics/tracking scripts where they are not required for visual behavior.
10. Keep only JavaScript required for menus, sliders, animations, accordions, and responsive behavior.

Visual sections to preserve:
- Header/top navigation
- Main navigation / mega-menu visual behavior if present
- Hero slider / homepage teaser section, Slider and similar elements
- Text and CTA buttons
- partnerstatus / award / badge section
- Expertise/cards section
- Footer with locations and legal/footer links

Quality requirements:
The page must be usable offline after the first clone step.
The local browser console should have no critical JavaScript errors.
The local page should not call analytics, tracking, forms, or remote APIs.
All links must point to <SAFE_LINK_TARGET>.
The clone should pass a basic visual comparison against the live homepage at desktop width 1440px and mobile width 390px.
Document known differences in README.md.

Cookie banner handling:
If a cookie banner, Cookiebot dialog, consent popup, privacy overlay, tracking preference modal, or cookie bar or similar thing appears during extraction or on first page load, ignore it for the clone.
Do not reproduce the cookie banner in the local version.
Do not clone Cookiebot, consent-management scripts, tracking-preference scripts, or related overlays.
Do not let the cookie popup affect screenshots, DOM extraction, layout capture, or visual comparison.
If necessary, dismiss or hide the cookie popup during extraction before saving the rendered DOM.
The final local Express app must load without any cookie banner, cookie modal, consent bar, or privacy popup.

Deliverables:
1. Complete working project files.
2. README.md with:
   - how to start the app
   - what was cloned
   - what was intentionally disabled
   - list of missing/unavailable assets, if any
   - known visual differences
3. A short final summary with:
   - exact commands to run
   - local URL
   - major limitations

Commands expected after completion:
npm install
npm start

Then open: 
http://localhost:3000

It should be accessible on the configured port and bind address. Use `HOST=0.0.0.0 PORT=3000 npm start` when access from other local network interfaces is required.
```
</details>
