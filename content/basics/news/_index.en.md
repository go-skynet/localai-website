+++
disableToc = false
title = "What's New"
weight = 1
+++


## 27-05-2023: __v1.16.0__ 

Now it's possible to automatically download pre-configured models before starting the API. 

[[ explain ]]

`llama.cpp` models now can also automatically save the prompt cache state as well by specifying a 

[[ explain ]

]

## Media, Blogs, Social

- [LocalAI meets k8sgpt](https://www.youtube.com/watch?v=PKrDNuJ_dfE) - CNCF Webinar showcasing LocalAI and k8sgpt.
- [Question Answering on Documents locally with LangChain, LocalAI, Chroma, and GPT4All](https://mudler.pm/posts/localai-question-answering/) by Ettore Di Giacinto
- [Tutorial to use k8sgpt with LocalAI](https://medium.com/@tyler_97636/k8sgpt-localai-unlock-kubernetes-superpowers-for-free-584790de9b65) - excellent usecase for localAI, using AI to analyse Kubernetes clusters. by Tyller Gillson

## Previous 

- 23-05-2023: __v1.15.0__ released. `go-gpt2.cpp` backend got renamed to `go-ggml-transformers.cpp` updated including https://github.com/ggerganov/llama.cpp/pull/1508 which breaks compatibility with older models. This impacts RedPajama, GptNeoX, MPT(not `gpt4all-mpt`), Dolly, GPT2 and Starcoder based models. [Binary releases available](https://github.com/go-skynet/LocalAI/releases), various fixes, including https://github.com/go-skynet/LocalAI/pull/341 .
- 21-05-2023: __v1.14.0__ released. Minor updates to the `/models/apply` endpoint, `llama.cpp` backend updated including https://github.com/ggerganov/llama.cpp/pull/1508 which breaks compatibility with older models. `gpt4all` is still compatible with the old format. 
- 19-05-2023: __v1.13.0__ released! 🔥🔥 updates to the `gpt4all` and `llama` backend, consolidated CUDA support ( https://github.com/go-skynet/LocalAI/pull/310 thanks to @bubthegreat and @Thireus ), preliminar support for [installing models via API](https://github.com/go-skynet/LocalAI#advanced-prepare-models-using-the-api).
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
