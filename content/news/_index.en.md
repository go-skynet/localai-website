+++
disableToc = false
title = "What's New"
weight = 2
url = '/basics/news/'

+++

## 🔥🔥🔥 23-07-2023: __v1.22.0__ 🚀

* feat: add llama-master backend by @mudler in https://github.com/go-skynet/LocalAI/pull/752
* [build] pass build type to cmake on libtransformers.a build by @TonDar0n in https://github.com/go-skynet/LocalAI/pull/741
* feat: resolve JSONSchema refs (planners) by @mudler in https://github.com/go-skynet/LocalAI/pull/774
* feat: backends improvements by @mudler in https://github.com/go-skynet/LocalAI/pull/778
* feat(llama2): add template for chat messages by @dave-gray101 in https://github.com/go-skynet/LocalAI/pull/782

{{% notice note %}}

From this release to use the OpenAI functions you need to use the `llama-grammar` backend. It has been added a `llama` backend for tracking `llama.cpp` master and `llama-grammar` for the grammar functionalities that have not been merged yet upstream. See also [OpenAI functions]({{%relref "features/openai-functions" %}}). Until the feature is merged we will have two llama backends.

{{% /notice %}}

## Huggingface embeddings

In this release is now possible to specify to LocalAI external `gRPC` backends that can be used for inferencing https://github.com/go-skynet/LocalAI/pull/778. It is now possible to write internal backends in any language, and a `huggingface-embeddings` backend is now available in the container image to be used with https://github.com/UKPLab/sentence-transformers. See also [Embeddings]({{%relref "features/embeddings" %}}).

## LLaMa 2 has been released!

Thanks to the community effort now LocalAI supports templating for LLaMa2! more at: https://github.com/go-skynet/LocalAI/pull/782 until we update the model gallery with LLaMa2 models!

## Official langchain integration

Progress has been made to support LocalAI with `langchain`. See: https://github.com/langchain-ai/langchain/pull/8134

## 🔥🔥🔥 17-07-2023: __v1.21.0__ 🚀

* [whisper] Partial support for verbose_json format in transcribe endpoint by `@ldotlopez` in https://github.com/go-skynet/LocalAI/pull/721
* LocalAI functions by `@mudler` in https://github.com/go-skynet/LocalAI/pull/726
* `gRPC`-based backends by `@mudler` in https://github.com/go-skynet/LocalAI/pull/743
* falcon support (7b and 40b) with `ggllm.cpp` by `@mudler` in https://github.com/go-skynet/LocalAI/pull/743

### LocalAI functions

This allows to run OpenAI functions as described in the OpenAI blog post and documentation: https://openai.com/blog/function-calling-and-other-api-updates.

This is a video of running the same example, locally with `LocalAI`:
![localai-functions-1](https://github.com/ggerganov/llama.cpp/assets/2420543/5bd15da2-78c1-4625-be90-1e938e6823f1)

And here when it actually picks to reply to the user instead of using functions!
![functions-2](https://github.com/ggerganov/llama.cpp/assets/2420543/e3f89d15-1d2c-45ab-974f-6c9eb8eae41d)

Note: functions are supported only with `llama.cpp`-compatible models.

A full example is available here: https://github.com/go-skynet/LocalAI/tree/master/examples/functions

### gRPC backends

This is an internal refactor which is not user-facing, however, it allows to ease out maintenance and addition of new backends to LocalAI!

### `falcon` support

Now Falcon 7b and 40b models compatible with https://github.com/cmp-nct/ggllm.cpp are supported as well.

The former, ggml-based backend has been renamed to `falcon-ggml`.

### Default pre-compiled binaries

From this release the default behavior of images has changed. Compilation is not triggered on start automatically, to recompile `local-ai` from scratch on start and switch back to the old behavior, you can set `REBUILD=true` in the environment variables. Rebuilding can be necessary if your CPU and/or architecture is old and the pre-compiled binaries are not compatible with your platform. See the [build section]({{%relref "build" %}}) for more information.

[Full release changelog](https://github.com/go-skynet/LocalAI/releases/tag/v1.21.0)

## 🔥🔥🔥 28-06-2023: __v1.20.0__ 🚀

### Exciting New Features 🎉

* Add Text-to-Audio generation with `go-piper` by @mudler in https://github.com/go-skynet/LocalAI/pull/649 See [API endpoints]({{%relref "features/text-to-audio" %}}) in our documentation.
* Add gallery repository by @mudler in https://github.com/go-skynet/LocalAI/pull/663. See [models]({{%relref "models" %}}) for documentation.

### Container images
- Standard (GPT + `stablediffusion`): `quay.io/go-skynet/local-ai:v1.20.0`
- FFmpeg: `quay.io/go-skynet/local-ai:v1.20.0-ffmpeg`
- CUDA 11+FFmpeg: `quay.io/go-skynet/local-ai:v1.20.0-cublas-cuda11-ffmpeg`
- CUDA 12+FFmpeg: `quay.io/go-skynet/local-ai:v1.20.0-cublas-cuda12-ffmpeg`

### Updates

Updates to `llama.cpp`, `go-transformers`, `gpt4all.cpp` and `rwkv.cpp`.

The NUMA option was enabled by @mudler in https://github.com/go-skynet/LocalAI/pull/684, along with many new parameters (`mmap`,`mmlock`, ..). See [advanced]({{%relref "advanced" %}}) for the full list of parameters.

### Gallery repositories

In this release there is support for gallery repositories. These are repositories that contain models, and can be used to install models. The default gallery which contains only freely licensed models is in Github: https://github.com/go-skynet/model-gallery, but you can use your own gallery by setting the `GALLERIES` environment variable. An automatic index of huggingface models is available as well.

For example, now you can start `LocalAI` with the following environment variable to use both galleries:

```bash
GALLERIES=[{"name":"model-gallery", "url":"github:go-skynet/model-gallery/index.yaml"}, {"url": "github:ci-robbot/localai-huggingface-zoo/index.yaml","name":"huggingface"}]
```

And in runtime you can install a model from huggingface now with:

```bash
curl http://localhost:8000/models/apply -H "Content-Type: application/json" -d '{ "id": "huggingface@thebloke__open-llama-7b-open-instruct-ggml__open-llama-7b-open-instruct.ggmlv3.q4_0.bin" }'
```

or a `tts` voice with:

```bash
curl http://localhost:8080/models/apply -H "Content-Type: application/json" -d '{ "id": "model-gallery@voice-en-us-kathleen-low" }'
```

See also [models]({{%relref "models" %}}) for a complete documentation.

### Text to Audio

Now `LocalAI` uses [piper](https://github.com/rhasspy/piper) and [go-piper](https://github.com/mudler/go-piper) to generate audio from text. This is an experimental feature, and it requires `GO_TAGS=tts` to be set during build. It is enabled by default in the pre-built container images.

To setup audio models, you can use the new galleries, or setup the models manually as described in [the API section of the documentation]({{%relref "features/text-to-audio" %}}).

You can check the full changelog in [Github](https://github.com/go-skynet/LocalAI/releases/tag/v1.20.0)

## 🔥🔥🔥 19-06-2023: __v1.19.0__ 🚀

- Full CUDA GPU offload support ( [PR](https://github.com/go-skynet/go-llama.cpp/pull/105) by [mudler](https://github.com/mudler). Thanks to [chnyda](https://github.com/chnyda) for handing over the GPU access, and [lu-zero](https://github.com/lu-zero) to help in debugging  )
- Full GPU Metal Support is now fully functional. Thanks to [Soleblaze](https://github.com/Soleblaze) to iron out the Metal Apple silicon support!

Container images:
- Standard (GPT + `stablediffusion`): `quay.io/go-skynet/local-ai:v1.19.2`
- FFmpeg: `quay.io/go-skynet/local-ai:v1.19.2-ffmpeg`
- CUDA 11+FFmpeg: `quay.io/go-skynet/local-ai:v1.19.2-cublas-cuda11-ffmpeg`
- CUDA 12+FFmpeg: `quay.io/go-skynet/local-ai:v1.19.2-cublas-cuda12-ffmpeg`

## 🔥🔥🔥 06-06-2023: __v1.18.0__ 🚀

This LocalAI release is plenty of new features, bugfixes and updates! Thanks to the community for the help, this was a great community release!

We now support a vast variety of models, while being backward compatible with prior quantization formats, this new release allows still to load older formats and new [k-quants](https://github.com/ggerganov/llama.cpp/pull/1684)!

### New features

- ✨ Added support for `falcon`-based model families (7b)  ( [mudler](https://github.com/mudler) )
- ✨ Experimental support for Metal Apple Silicon GPU - ( [mudler](https://github.com/mudler) and thanks to [Soleblaze](https://github.com/Soleblaze) for testing! ). See the [build section]({{%relref "build#Acceleration" %}}).
- ✨ Support for token stream in the `/v1/completions` endpoint ( [samm81](https://github.com/samm81) )
- ✨ Added huggingface backend ( [Evilfreelancer](https://github.com/EvilFreelancer) )
- 📷 Stablediffusion now can output `2048x2048` images size with `esrgan`! ( [mudler](https://github.com/mudler) )

### Container images
- 🐋 CUDA container images (arm64, x86_64) ( [sebastien-prudhomme](https://github.com/sebastien-prudhomme) )
- 🐋 FFmpeg container images (arm64, x86_64) ( [mudler](https://github.com/mudler) )

### Dependencies updates

- 🆙 Bloomz has been updated to the latest ggml changes, including new quantization format ( [mudler](https://github.com/mudler) )
- 🆙 RWKV has been updated to the new quantization format( [mudler](https://github.com/mudler) )
- 🆙 [k-quants](https://github.com/ggerganov/llama.cpp/pull/1684) format support for the `llama` models ( [mudler](https://github.com/mudler) )
- 🆙 gpt4all has been updated, incorporating upstream changes allowing to load older models, and with different CPU instruction set (AVX only, AVX2) from the same binary! ( [mudler](https://github.com/mudler) )

### Generic

- 🐧 Fully Linux static binary releases ( [mudler](https://github.com/mudler) )
- 📷 Stablediffusion has been enabled on container images by default ( [mudler](https://github.com/mudler) )
  Note: You can disable container image rebuilds with `REBUILD=false`

### Examples

- 💡 [AutoGPT](https://github.com/go-skynet/LocalAI/tree/master/examples/autoGPT) example ( [mudler](https://github.com/mudler) )
- 💡 [PrivateGPT](https://github.com/go-skynet/LocalAI/tree/master/examples/privateGPT) example ( [mudler](https://github.com/mudler) )
- 💡 [Flowise](https://github.com/go-skynet/LocalAI/tree/master/examples/flowise) example ( [mudler](https://github.com/mudler) )

Two new projects offer now direct integration with LocalAI!

- [Flowise](https://github.com/FlowiseAI/Flowise/pull/123)
- [Mods](https://github.com/charmbracelet/mods)

[Full release changelog](https://github.com/go-skynet/LocalAI/releases/tag/v1.18.0)

## 29-05-2023: __v1.17.0__

Support for OpenCL has been added while building from sources.

You can now build LocalAI from source with `BUILD_TYPE=clblas` to have an OpenCL build. See also the [build section]({{%relref "build#Acceleration" %}}).

For instructions on how to install OpenCL/CLBlast see [here](https://github.com/ggerganov/llama.cpp#blas-build).

rwkv.cpp has been updated to the new ggml format [commit](https://github.com/saharNooby/rwkv.cpp/commit/dea929f8cad90b7cf2f820c5a3d6653cfdd58c4e).

## 27-05-2023: __v1.16.0__ 

Now it's possible to automatically download pre-configured models before starting the API. 

Start local-ai with the `PRELOAD_MODELS` containing a list of models from the gallery, for instance to install `gpt4all-j` as `gpt-3.5-turbo`:

```bash
PRELOAD_MODELS=[{"url": "github:go-skynet/model-gallery/gpt4all-j.yaml", "name": "gpt-3.5-turbo"}]
```

`llama.cpp` models now can also automatically save the prompt cache state as well by specifying in the model YAML configuration file:

```yaml
# Enable prompt caching

# This is a file that will be used to save/load the cache. relative to the models directory.
prompt_cache_path: "alpaca-cache"

# Always enable prompt cache
prompt_cache_all: true
```

See also the [advanced section]({{%relref "advanced" %}}).

## Media, Blogs, Social

- [Create a slackbot for teams and OSS projects that answer to documentation](https://mudler.pm/posts/smart-slackbot-for-teams/)
- [LocalAI meets k8sgpt](https://www.youtube.com/watch?v=PKrDNuJ_dfE) - CNCF Webinar showcasing LocalAI and k8sgpt.
- [Question Answering on Documents locally with LangChain, LocalAI, Chroma, and GPT4All](https://mudler.pm/posts/localai-question-answering/) by Ettore Di Giacinto
- [Tutorial to use k8sgpt with LocalAI](https://medium.com/@tyler_97636/k8sgpt-localai-unlock-kubernetes-superpowers-for-free-584790de9b65) - excellent usecase for localAI, using AI to analyse Kubernetes clusters. by Tyller Gillson

## Previous 

- 23-05-2023: __v1.15.0__ released. `go-gpt2.cpp` backend got renamed to `go-ggml-transformers.cpp` updated including https://github.com/ggerganov/llama.cpp/pull/1508 which breaks compatibility with older models. This impacts RedPajama, GptNeoX, MPT(not `gpt4all-mpt`), Dolly, GPT2 and Starcoder based models. [Binary releases available](https://github.com/go-skynet/LocalAI/releases), various fixes, including https://github.com/go-skynet/LocalAI/pull/341 .
- 21-05-2023: __v1.14.0__ released. Minor updates to the `/models/apply` endpoint, `llama.cpp` backend updated including https://github.com/ggerganov/llama.cpp/pull/1508 which breaks compatibility with older models. `gpt4all` is still compatible with the old format. 
- 19-05-2023: __v1.13.0__ released! 🔥🔥 updates to the `gpt4all` and `llama` backend, consolidated CUDA support ( https://github.com/go-skynet/LocalAI/pull/310 thanks to @bubthegreat and @Thireus ), preliminar support for [installing models via API]({{%relref "advanced#" %}}).
- 17-05-2023:  __v1.12.0__ released! 🔥🔥 Minor fixes, plus CUDA (https://github.com/go-skynet/LocalAI/pull/258) support for `llama.cpp`-compatible models and image generation (https://github.com/go-skynet/LocalAI/pull/272).
- 16-05-2023: 🔥🔥🔥 Experimental support for CUDA (https://github.com/go-skynet/LocalAI/pull/258) in the `llama.cpp` backend and Stable diffusion CPU image generation (https://github.com/go-skynet/LocalAI/pull/272) in `master`.

Now LocalAI can generate images too:

| mode=0                                                                                                                | mode=1 (winograd/sgemm)                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| ![b6441997879](https://github.com/go-skynet/LocalAI/assets/2420543/d50af51c-51b7-4f39-b6c2-bf04c403894c)              | ![winograd2](https://github.com/go-skynet/LocalAI/assets/2420543/1935a69a-ecce-4afc-a099-1ac28cb649b3)                |

- 14-05-2023: __v1.11.1__ released! `rwkv` backend patch release
- 13-05-2023: __v1.11.0__ released! 🔥 Updated `llama.cpp` bindings: This update includes a breaking change in the model files ( https://github.com/ggerganov/llama.cpp/pull/1405 ) - old models should still work with the `gpt4all-llama` backend.
- 12-05-2023: __v1.10.0__ released! 🔥🔥 Updated `gpt4all` bindings. Added support for GPTNeox (experimental), RedPajama (experimental), Starcoder (experimental), Replit (experimental), MosaicML MPT. Also now `embeddings` endpoint supports tokens arrays. See the [langchain-chroma](https://github.com/go-skynet/LocalAI/tree/master/examples/langchain-chroma) example! Note - this update does NOT include https://github.com/ggerganov/llama.cpp/pull/1405 which makes models incompatible.
- 11-05-2023: __v1.9.0__ released! 🔥 Important whisper updates ( https://github.com/go-skynet/LocalAI/pull/233 https://github.com/go-skynet/LocalAI/pull/229 ) and extended gpt4all model families support ( https://github.com/go-skynet/LocalAI/pull/232 ). Redpajama/dolly experimental ( https://github.com/go-skynet/LocalAI/pull/214 )
- 10-05-2023: __v1.8.0__ released! 🔥 Added support for fast and accurate embeddings with `bert.cpp` ( https://github.com/go-skynet/LocalAI/pull/222 )
- 09-05-2023: Added experimental support for transcriptions endpoint ( https://github.com/go-skynet/LocalAI/pull/211 )
- 08-05-2023: Support for embeddings with models using the `llama.cpp` backend ( https://github.com/go-skynet/LocalAI/pull/207 )
- 02-05-2023: Support for `rwkv.cpp` models ( https://github.com/go-skynet/LocalAI/pull/158 ) and for `/edits` endpoint
- 01-05-2023: Support for SSE stream of tokens in `llama.cpp` backends ( https://github.com/go-skynet/LocalAI/pull/152 )
