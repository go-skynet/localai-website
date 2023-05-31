
+++
disableToc = false
title = "Model compatibility"
weight = 2
+++

LocalAI is compatible with the models supported by [llama.cpp](https://github.com/ggerganov/llama.cpp) supports also [GPT4ALL-J](https://github.com/nomic-ai/gpt4all) and [cerebras-GPT with ggml](https://huggingface.co/lxe/Cerebras-GPT-2.7B-Alpaca-SP-ggml).

Tested with:

- [X] LLaMA 🦙
- [X] [Vicuna](https://github.com/ggerganov/llama.cpp/discussions/643#discussioncomment-5533894)
- [Alpaca](https://github.com/ggerganov/llama.cpp#instruction-mode-with-alpaca)
- [X] [GPT4ALL](https://gpt4all.io) (see also [using GPT4All](https://github.com/ggerganov/llama.cpp#using-gpt4all))
- [X] [GPT4ALL-J](https://gpt4all.io/models/ggml-gpt4all-j.bin) (no changes required)
- [X] [Koala](https://bair.berkeley.edu/blog/2023/04/03/koala/) 🐨
- [X] Cerebras-GPT
- [X] [WizardLM](https://github.com/nlpxucan/WizardLM)
- [X] [RWKV](https://github.com/BlinkDL/RWKV-LM) models with [rwkv.cpp](https://github.com/saharNooby/rwkv.cpp)
- [X] [bloom.cpp](https://github.com/NouamaneTazi/bloomz.cpp)
- [X] [Chinese LLaMA / Alpaca](https://github.com/ymcui/Chinese-LLaMA-Alpaca)
- [X] [Vigogne (French)](https://github.com/bofenghuang/vigogne)
- [X] [OpenBuddy 🐶 (Multilingual)](https://github.com/OpenBuddy/OpenBuddy)
- [X] [Pygmalion 7B / Metharme 7B](https://github.com/ggerganov/llama.cpp#using-pygmalion-7b--metharme-7b)
- [X] [HuggingFace Inference](https://huggingface.co/inference-api) models available through API


Note: You might need to convert some models from older models to the new format, for indications, see [the README in llama.cpp](https://github.com/ggerganov/llama.cpp#using-gpt4all) for instance to run `gpt4all`.

### RWKV

A full example on how to run a rwkv model is in the [examples](https://github.com/go-skynet/LocalAI/tree/master/examples/rwkv).

Note: rwkv models needs to specify the backend `rwkv` in the YAML config files and have an associated tokenizer along that needs to be provided with it:

```
36464540 -rw-r--r--  1 mudler mudler 1.2G May  3 10:51 rwkv_small
36464543 -rw-r--r--  1 mudler mudler 2.4M May  3 10:51 rwkv_small.tokenizer.json
```

### Hardware requirements

Depending on the model you are attempting to run might need more RAM or CPU resources. Check out also [here](https://github.com/ggerganov/llama.cpp#memorydisk-requirements) for `ggml` based backends. `rwkv` is less expensive on resources.


### Model compatibility table

Besides llama based models, LocalAI is compatible also with other architectures. The table below lists all the compatible models families and the associated binding repository.

| Backend and Bindings                                                                                                           | Compatible models                                        | Completion/Chat endpoint | Audio transcription/Image | Embeddings support                | Token stream support |
|--------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------|--------------------------|---------------------------|-----------------------------------|----------------------|
| [llama](https://github.com/ggerganov/llama.cpp) ([binding](https://github.com/go-skynet/go-llama.cpp))                         | Vicuna, Alpaca, LLaMa                                    | yes                      | no                        | yes (doesn't seem to be accurate) | yes                  |
| [gpt4all-llama](https://github.com/nomic-ai/gpt4all)                                                                           | Vicuna, Alpaca, LLaMa                                    | yes                      | no                        | no                                | yes                  |
| [gpt4all-mpt](https://github.com/nomic-ai/gpt4all)                                                                             | MPT                                                      | yes                      | no                        | no                                | yes                  |
| [gpt4all-j](https://github.com/nomic-ai/gpt4all)                                                                               | GPT4ALL-J                                                | yes                      | no                        | no                                | yes                  |
| [gpt2](https://github.com/ggerganov/ggml) ([binding](https://github.com/go-skynet/go-ggml-transformers.cpp))                   | GPT2, Cerebras                                           | yes                      | no                        | no                                | no                   |
| [dolly](https://github.com/ggerganov/ggml) ([binding](https://github.com/go-skynet/go-ggml-transformers.cpp))                  | Dolly                                                    | yes                      | no                        | no                                | no                   |
| [gptj](https://github.com/ggerganov/ggml) ([binding](https://github.com/go-skynet/go-ggml-transformers.cpp))                   | GPTJ                                                     | yes                      | no                        | no                                | no                   |
| [mpt](https://github.com/ggerganov/ggml) ([binding](https://github.com/go-skynet/go-ggml-transformers.cpp))                    | MPT                                                      | yes                      | no                        | no                                | no                   |
| [replit](https://github.com/ggerganov/ggml) ([binding](https://github.com/go-skynet/go-ggml-transformers.cpp))                 | Replit                                                   | yes                      | no                        | no                                | no                   |
| [gptneox](https://github.com/ggerganov/ggml) ([binding](https://github.com/go-skynet/go-ggml-transformers.cpp))                | GPT NeoX, RedPajama, StableLM                            | yes                      | no                        | no                                | no                   |
| [starcoder](https://github.com/ggerganov/ggml) ([binding](https://github.com/go-skynet/go-ggml-transformers.cpp))              | Starcoder                                                | yes                      | no                        | no                                | no                   |
| [bloomz](https://github.com/NouamaneTazi/bloomz.cpp) ([binding](https://github.com/go-skynet/bloomz.cpp))                      | Bloom                                                    | yes                      | no                        | no                                | no                   |
| [rwkv](https://github.com/saharNooby/rwkv.cpp) ([binding](https://github.com/donomii/go-rw))                                   | rwkv                                                     | yes                      | no                        | no                                | yes                  |
| [bert](https://github.com/skeskinen/bert.cpp) ([binding](https://github.com/go-skynet/go-bert.cpp))                            | bert                                                     | no                       | no                        | yes                               | no                   |    
| [whisper](https://github.com/ggerganov/whisper.cpp)                                                                            | whisper                                                  | no                       | Audio                     | no                                | no                   |  
| [stablediffusion](https://github.com/EdVince/Stable-Diffusion-NCNN) ([binding](https://github.com/mudler/go-stable-diffusion)) | stablediffusion                                          | no                       | Image                     | no                                | no                   | 
| [langchain-huggingface](https://github.com/tmc/langchaingo)                                                                    | Any text generators available on HuggingFace through API | yes                      | no                        | no                                | no                   |
