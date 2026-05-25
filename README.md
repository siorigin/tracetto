# Tracetto Documentation

**Language / 语言:** [简体中文](./README_zh-CN.md) | English

[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](./LICENSE)
[![Website](https://img.shields.io/badge/try-tracetto.com-2ea44f.svg)](https://tracetto.com)

Tracetto is a browser-side analysis tool for PyTorch Profiler traces. It helps algorithm and performance engineers move from "I have a trace file" to "I know where the bottleneck is" by summarizing GPU time, operator hotspots, kernel behavior, memory movement, and distributed workload imbalance.

Tracetto parses trace files locally in your browser. No trace data needs to be uploaded to a server.

![Tracetto import page](./en/images/home.png)

## Start Here

- Open Tracetto: [https://tracetto.com](https://tracetto.com)
- Quickstart: [en/quickstart.md](./en/quickstart.md)
- Reference: [en/reference.md](./en/reference.md)

## What Tracetto Helps You Answer

- Is GPU time spent on compute, communication, memory copy, or idle gaps?
- Which PyTorch operators and GPU kernels are the real hotspots?
- Is CPU launch overhead slowing down GPU execution?
- Are multi-rank workloads imbalanced?
- Is communication effectively overlapped with compute?
- Which phase, module, operator, or call stack should be investigated next?

## Supported Trace Files

Tracetto works with PyTorch Profiler Chrome Trace exports, including:

- `.json`
- `.json.gz`

You can generate compatible traces from plain PyTorch programs, vLLM, SGLang, and other systems that export PyTorch Profiler traces.

## Documentation

| Document                      | Description                                                                                       |
| ----------------------------- | ------------------------------------------------------------------------------------------------- |
| [Quickstart](./en/quickstart.md) | First-use guide covering trace collection, import, timeline selection, and an end-to-end analysis |
| [Reference](./en/reference.md)   | Day-to-day reference for each view, common analysis workflows, export behavior, and FAQ           |

For the Simplified Chinese version, see [README_zh-CN.md](./README_zh-CN.md), [中文快速上手](./zh-CN/quickstart.md), and [中文参考手册](./zh-CN/reference.md).

## Analysis Workflow

1. Generate a PyTorch Profiler trace.
2. Open [tracetto.com](https://tracetto.com) and import one or more trace files.
3. Use `Timeline Overview` to select the phase or module you care about.
4. Check `Overview` for the compute / non-compute / idle breakdown.
5. Drill into `Operator View`, `Kernel View`, `Memory View`, or `Distributed View`.
6. Use `Call Stack` to connect expensive kernels or events back to Python and framework code.

Tracetto is designed to complement Perfetto: use Tracetto to quickly narrow down where and why a workload is slow, then use Perfetto for event-level timeline inspection when needed.

## Repository Layout

```text
.
├── en/              English documentation and images
├── zh-CN/           Simplified Chinese documentation and images
├── LICENSE          Apache-2.0 license
├── README.md        English README
└── README_zh-CN.md  Simplified Chinese README
```

## Data Privacy

Trace files may contain model names, file paths, operator names, shapes, timing information, and other workload metadata. Tracetto performs parsing and analysis in the browser, so files selected through the Web UI stay on your local machine during analysis.

## Feedback and Contributions

Issues, corrections, and documentation improvements are welcome. When reporting a problem, please include:

- The browser and operating system you used
- Whether the trace is single-rank or multi-rank
- The approximate trace size and file extension
- A screenshot or short description of the view where the issue appears

Please avoid sharing private trace files publicly unless they have been sanitized.

## License

This repository is licensed under the [Apache License 2.0](./LICENSE).
