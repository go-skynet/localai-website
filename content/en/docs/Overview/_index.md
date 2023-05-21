---
title: "Overview"
linkTitle: "Overview"
weight: 1
description: >
  Overview
---

{{% pageinfo %}}
📢 LocalAI v1.14.0 is here! This release brings compatibility with the latest quantization method updates from llama.cpp while maintaining support for older models!
{{% /pageinfo %}}


LocalAI is a drop-in replacement REST API compatible with OpenAI for local CPU inferencing. It allows you to run models locally or on-prem with consumer grade hardware, supporting multiple models families. LocalAI is a community-driven project, focused on making the AI accessible to anyone.

LocalAI uses C++ bindings for optimizing speed and performance. It is based on llama.cpp gpt4all, rwkv.cpp, ggml, whisper.cpp for audio transcriptions, and bert.cpp for embedding. LocalAI also supports GPT4ALL-J which is licensed under Apache 2.0, and MosaicLM PT models which are also usable for commercial applications. (see here the table of supported models)

To use LocalAI, you need to install it on your machine and run it as a service, or either on the cloud or in a dedicated environment. You can then use the same API endpoints as OpenAI to interact with the models. For example, you can use the /v1/models endpoint to list the available models, or the /v1/completions endpoint to generate text completions, but computation is executed locally, with CPU-compatible models. You can download models from Gpt4all.

LocalAI also supports various ranges of configuration and prompt templates, which are predefined prompts that can help you generate specific outputs with the models. For example, you can use the summarizer template to generate summaries of texts, or the sentiment-analyzer template to analyze the sentiment of texts. You can find more examples and prompt templates in the LocalAI repository.


## LocalAI

🤖 Self-hosted, community-driven, local OpenAI-compatible API. Drop-in replacement for OpenAI running LLMs on consumer-grade hardware. No GPU required. LocalAI is a RESTful API to run ggml compatible models: llama.cpp, alpaca.cpp, gpt4all.cpp, rwkv.cpp, whisper.cpp, vicuna, koala, gpt4all-j, cerebras and many others!


## Models Gallery

The model gallery is a curated collection of models created by the community and tested with LocalAI.


## Where should I go next?

* [Getting Started](/docs/getting-started/): Get started with $project
* [Examples](/docs/examples/): Check out some example code!

