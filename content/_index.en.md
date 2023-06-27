+++
archetype = "home"
title = "LocalAI"
+++

<a href="https://github.com/go-skynet/LocalAI/actions/workflows/test.yml"><img src="https://github.com/go-skynet/LocalAI/actions/workflows/test.yml/badge.svg"></a><a href="https://github.com/go-skynet/LocalAI/actions/workflows/image.yml"><img src="https://github.com/go-skynet/LocalAI/actions/workflows/image.yml/badge.svg"></a><a href="https://discord.gg/uJAeKSAGDy"><img src="https://dcbadge.vercel.app/api/server/uJAeKSAGDy?style=flat-square&theme=default-inverted"></a>

**LocalAI** is a drop-in replacement REST API that's compatible with OpenAI API specifications for local inferencing. It allows you to run LLMs (and not only) locally or on-prem with consumer grade hardware, supporting multiple model families that are compatible with the ggml format. Does not require GPU.

For a list of the supported model families, see [Model compatibility]({{%relref "model-compatibility" %}}).

In a nutshell:

- Local, OpenAI drop-in alternative REST API. You own your data.
- NO GPU required. NO Internet access is required either
  - Optional, GPU Acceleration is available in `llama.cpp`-compatible LLMs. See also the [build section]({{%relref "basics/build" %}}). 
- Supports multiple models: 
  - 🗣 Text to Audio 🎺🆕
  - 🔈 Audio to Text (Audio transcription with `whisper.cpp`)
  - 📖 Text generation with GPTs (`llama.cpp`, `gpt4all.cpp`, ... and more)
  - 🎨 Image generation with stable diffusion
- 🏃 Once loaded the first time, it keep models loaded in memory for faster inference
- ⚡ Doesn't shell-out, but uses C++ bindings for a faster inference and better performance. 

LocalAI was created by [Ettore Di Giacinto](https://github.com/mudler/) and is a community-driven project, focused on making the AI accessible to anyone. Any contribution, feedback and PR is welcome! 



| [ChatGPT OSS alternative](https://github.com/go-skynet/LocalAI/tree/master/examples/chatbot-ui)                                                                                                                | [Image generation](https://localai.io/api-endpoints/index.html#image-generation)                                                                                                              |
|------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
|  ![Screenshot from 2023-04-26 23-59-55](https://user-images.githubusercontent.com/2420543/234715439-98d12e03-d3ce-4f94-ab54-2b256808e05e.png)            | ![b6441997879](https://github.com/go-skynet/LocalAI/assets/2420543/d50af51c-51b7-4f39-b6c2-bf04c403894c)                  |


See the [Getting started]({{%relref "basics/getting_started" %}}) and [examples](https://github.com/go-skynet/LocalAI/tree/master/examples/) sections to learn how to use LocalAI. For a list of curated models check out the [model gallery](https://github.com/go-skynet/model-gallery).

## How does it work?  

<details>

LocalAI is an API written in Go that serves as an OpenAI shim, enabling software already developed with OpenAI SDKs to seamlessly integrate with LocalAI. It can be effortlessly implemented as a substitute, even on consumer-grade hardware. This capability is achieved by employing various C++ backends, including [ggml](https://github.com/ggerganov/ggml), to perform inference on LLMs using both CPU and, if desired, GPU.

LocalAI uses C++ bindings for optimizing speed. It is based on [llama.cpp](https://github.com/ggerganov/llama.cpp), [gpt4all](https://github.com/nomic-ai/gpt4all), [rwkv.cpp](https://github.com/saharNooby/rwkv.cpp), [ggml](https://github.com/ggerganov/ggml), [whisper.cpp](https://github.com/ggerganov/whisper.cpp) for audio transcriptions, [bert.cpp](https://github.com/skeskinen/bert.cpp) for embedding and [StableDiffusion-NCN](https://github.com/EdVince/Stable-Diffusion-NCNN) for image generation. See [the model compatibility table]({{%relref "model-compatibility" %}}) to learn about all the components of LocalAI.

![LocalAI](https://github.com/go-skynet/LocalAI/assets/2420543/38de3a9b-3866-48cd-9234-662f9571064a)

</details>

## Contribute and help

To help the project you can:

- Upvote the [Reddit post](https://www.reddit.com/r/selfhosted/comments/12w4p2f/localai_openai_compatible_api_to_run_llm_models/) about LocalAI.

- [Hacker news post](https://news.ycombinator.com/item?id=35726934) - help us out by voting if you like this project.

- If you have technological skills and want to contribute to development, have a look at the open issues. If you are new you can have a look at the [good-first-issue](https://github.com/go-skynet/LocalAI/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) and [help-wanted](https://github.com/go-skynet/LocalAI/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) labels.

- If you don't have technological skills you can still help improving documentation or add examples or share your user-stories with our community, any help and contribution is welcome!

## License

LocalAI is licensed under the MIT License.


## Projects already using LocalAI to run local models

Feel free to open up a PR to get your project listed!

- [Kairos](https://github.com/kairos-io/kairos)
- [k8sgpt](https://github.com/k8sgpt-ai/k8sgpt#running-local-models)
- [Spark](https://github.com/cedriking/spark)
- [autogpt4all](https://github.com/aorumbayev/autogpt4all)
- [Mods](https://github.com/charmbracelet/mods)

## Short-term roadmap

- [x] Mimic OpenAI API (https://github.com/go-skynet/LocalAI/issues/10)
- [x] Binary releases (https://github.com/go-skynet/LocalAI/issues/6)
- [ ] Upstream our golang bindings to llama.cpp (https://github.com/ggerganov/llama.cpp/issues/351) 
- [x] Upstream [gpt4all](https://github.com/go-skynet/LocalAI/issues/85) bindings
- [x] Multi-model support
- [x] Have a webUI!
- [x] Allow configuration of defaults for models.
- [x] Support for embeddings
- [x] Support for audio transcription with https://github.com/ggerganov/whisper.cpp
- [x] GPU/CUDA support ( https://github.com/go-skynet/LocalAI/issues/69 )
- [X] Enable automatic downloading of models from a curated gallery
- [ ] Enable automatic downloading of models from HuggingFace
- [ ] Enable gallery management directly from the webui.

## Star history

[![LocalAI Star history Chart](https://api.star-history.com/svg?repos=go-skynet/LocalAI&type=Date)](https://star-history.com/#go-skynet/LocalAI&Date)

## Acknowledgements

LocalAI couldn't have been built without the help of great software already available from the community. Thank you!

- [llama.cpp](https://github.com/ggerganov/llama.cpp)
- https://github.com/tatsu-lab/stanford_alpaca
- https://github.com/cornelk/llama-go for the initial ideas
- https://github.com/antimatter15/alpaca.cpp
- https://github.com/EdVince/Stable-Diffusion-NCNN
- https://github.com/ggerganov/whisper.cpp
- https://github.com/saharNooby/rwkv.cpp

## License

LocalAI is a community-driven project created by [Ettore Di Giacinto](https://github.com/mudler/).

MIT

## Author

Ettore Di Giacinto and others

## Contributors

<a href="https://github.com/go-skynet/LocalAI/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=go-skynet/LocalAI" />
</a>
