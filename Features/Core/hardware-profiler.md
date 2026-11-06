# Hardware Profiler

**Release:** ATLAS Core  
**Status:** Planned  
**Category:** System capability assessment

## 1. Purpose

Hardware Profiler collects a practical overview of the computer's hardware and uses it to help users understand whether development tools and AI models are likely to run comfortably. It should make technical constraints understandable without pretending to provide perfect performance predictions.

## 2. Information to detect

Where supported by the operating system, collect:

- CPU model, architecture, logical processor count and relevant instruction-set capabilities.
- Installed and currently available system memory.
- GPU model and available graphics-memory information.
- Whether graphics memory is dedicated, shared or unified, where detectable.
- Storage capacity and available space on relevant volumes.
- Operating system and version.
- Virtualisation or subsystem information relevant to development, such as WSL or container availability, when detectable.

Do not infer unsupported details from marketing names. Show unavailable fields as unknown rather than guessing.

## 3. Presentation

Provide a readable system summary and a detailed technical view. Explain terms such as dedicated VRAM, shared memory, quantization and offloading when they affect a recommendation. Distinguish installed capacity from currently available resources and report when values were last measured.

## 4. Model and tool compatibility

When AI Model Manager or Developer Tool Manager asks for an assessment, compare known requirements with detected hardware. Consider memory requirements, model quantization, context size, CPU/GPU execution and storage. A recommendation should include:

- What is known about the model/tool requirement.
- What ATLAS detected.
- Which constraint may be limiting.
- Whether the result is a rough estimate or a verified compatibility rule.
- Potential alternatives, if known.

Never guarantee a model will run well based only on total RAM or a GPU name. Runtime, context length, concurrent applications, drivers and memory offload all matter.

## 5. Refresh and performance

Hardware detection should be lightweight and run on demand or at sensible intervals. Do not continuously benchmark the machine. A benchmark, if ever added, must be an explicit separate action with an explanation of load and duration.

## 6. Privacy

Hardware information remains local by default. Share only the minimum required facts with a cloud AI provider, and disclose that sharing when it occurs. Do not collect serial numbers or other unnecessary device identifiers.

## 7. Acceptance criteria

- Supported hardware fields are detected and labelled with source/time.
- Unknown values are not fabricated.
- Available memory is distinguished from installed memory.
- Compatibility assessments explain their assumptions and uncertainty.
- No benchmark or stress test runs automatically.
- Hardware data is not uploaded without disclosure and consent.

## 8. Dependencies and open decisions

Feeds AI Model Manager and Developer Tool Manager. Choose platform-specific detection libraries only after testing on supported operating systems. Define how stale readings are refreshed and which metrics are reliable on virtualised systems.

## 9. Related documentation

- [AI Model Manager](ai-model-manager.md)
- [Developer Tool Manager](developer-tool-manager.md)
- [System Monitor](system-monitor.md)
- [Master specification](../../ATLAS_MASTER_SPEC.md)
