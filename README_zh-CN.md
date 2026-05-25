# Tracetto 文档

**语言 / Language:** 简体中文 | [English](./README.md)

[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](./LICENSE)
[![Website](https://img.shields.io/badge/try-tracetto.com-2ea44f.svg)](https://tracetto.com)

Tracetto 是面向 PyTorch Profiler trace 的浏览器端分析工具，帮助算法工程师和性能工程师从一份 trace 文件快速定位 GPU 时间分布、operator 热点、kernel 行为、内存搬运和多 rank 负载不均等问题。

Tracetto 在浏览器内本地解析 trace 文件，无需上传数据。

![Tracetto 浏览器导入页](./zh-CN/images/home.png)

## 快速入口

- 在线使用：[https://tracetto.com](https://tracetto.com)
- 快速上手：[zh-CN/quickstart.md](./zh-CN/quickstart.md)
- 参考手册：[zh-CN/reference.md](./zh-CN/reference.md)

## 适用问题

- GPU 时间主要耗在计算、通信、内存搬运还是空闲？
- 哪些 PyTorch operator 和 GPU kernel 是真正热点？
- CPU launch 开销是否拖慢了 GPU？
- 多 rank 之间是否负载不均？
- 通信是否被计算有效 overlap？
- 下一步应该追到哪个阶段、模块、operator 或调用栈？

## 支持的 Trace 文件

Tracetto 支持 PyTorch Profiler 导出的 Chrome Trace 格式，包括：

- `.json`
- `.json.gz`

你可以从普通 PyTorch 程序、vLLM、SGLang 以及其他能导出 PyTorch Profiler trace 的系统中生成兼容文件。

## 文档导航

| 文档                           | 说明                                                                  |
| ------------------------------ | --------------------------------------------------------------------- |
| [快速上手](./zh-CN/quickstart.md) | 适合第一次使用，覆盖 trace 采集、文件导入、时间线选区和端到端分析流程 |
| [参考手册](./zh-CN/reference.md)  | 适合日常查阅，包含各视图说明、常见分析路径、导出说明和 FAQ            |

英文版本请见 [README.md](./README.md)、[English Quickstart](./en/quickstart.md) 和 [English Reference](./en/reference.md)。

## 典型分析流程

1. 生成 PyTorch Profiler trace。
2. 打开 [tracetto.com](https://tracetto.com)，导入一个或多个 trace 文件。
3. 使用 `Timeline Overview` 选择要分析的阶段或模块。
4. 在 `Overview` 查看 compute / non-compute / idle 时间分布。
5. 进入 `Operator View`、`Kernel View`、`Memory View` 或 `Distributed View` 下钻。
6. 使用 `Call Stack` 把高耗时 kernel 或 event 追溯到 Python / 框架调用路径。

Tracetto 适合与 Perfetto 配合使用：先用 Tracetto 快速收敛“哪里慢、为什么慢”，必要时再用 Perfetto 做事件级时间线验证。

## 仓库结构

```text
.
├── en/              English documentation and images
├── zh-CN/           简体中文文档与图片
├── LICENSE          Apache-2.0 license
├── README.md        English README
└── README_zh-CN.md  简体中文 README
```

## 数据隐私

Trace 文件可能包含模型名、文件路径、operator 名称、shape、耗时信息以及其他 workload 元数据。Tracetto 在浏览器内完成解析和分析，通过 Web UI 选择的文件会留在你的本地机器上。

## 反馈与贡献

欢迎提交 issue、修正文档或补充说明。反馈问题时，建议包含：

- 使用的浏览器和操作系统
- trace 是单 rank 还是多 rank
- trace 文件的大致大小和扩展名
- 问题出现在哪个视图，以及截图或简短描述

请避免公开上传未经脱敏的私有 trace 文件。

## 许可证

本仓库基于 [Apache License 2.0](./LICENSE) 发布。
