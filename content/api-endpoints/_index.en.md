

+++
disableToc = false
title = "API Endpoints"
weight = 2
+++

## Supported OpenAI API endpoints

You can check out the [OpenAI API reference](https://platform.openai.com/docs/api-reference/chat/create). 

Following the list of endpoints/parameters supported. 

Note:

- You can also specify the model as part of the OpenAI token.
- If only one model is available, the API will use it for all the requests.

### Chat completions

For example, to generate a chat completion, you can send a POST request to the `/v1/chat/completions` endpoint with the instruction as the request body:

```
curl http://localhost:8080/v1/chat/completions -H "Content-Type: application/json" -d '{
     "model": "ggml-koala-7b-model-q4_0-r2.bin",
     "messages": [{"role": "user", "content": "Say this is a test!"}],
     "temperature": 0.7
   }'
```

Available additional parameters: `top_p`, `top_k`, `max_tokens`

### Edit completions

To generate an edit completion you can send a POST request to the `/v1/edits` endpoint with the instruction as the request body:

```
curl http://localhost:8080/v1/edits -H "Content-Type: application/json" -d '{
     "model": "ggml-koala-7b-model-q4_0-r2.bin",
     "instruction": "rephrase",
     "input": "Black cat jumped out of the window",
     "temperature": 0.7
   }'
```

Available additional parameters: `top_p`, `top_k`, `max_tokens`.


### Completions

To generate a completion, you can send a POST request to the `/v1/completions` endpoint with the instruction as per the request body:

```
curl http://localhost:8080/v1/completions -H "Content-Type: application/json" -d '{
     "model": "ggml-koala-7b-model-q4_0-r2.bin",
     "prompt": "A long time ago in a galaxy far, far away",
     "temperature": 0.7
   }'
```

Available additional parameters: `top_p`, `top_k`, `max_tokens`

### List models

You can list all the models available with:

```
curl http://localhost:8080/v1/models
```

### Embeddings

OpenAI docs: https://platform.openai.com/docs/api-reference/embeddings

The embedding endpoint is experimental and enabled only if the model is configured with `embeddings: true` in its `yaml` file, for example:

```yaml
name: text-embedding-ada-002
parameters:
  model: bert
embeddings: true
backend: "bert-embeddings"
```

There is an example available [here](https://github.com/go-skynet/LocalAI/tree/master/examples/query_data/).

Note: embeddings is supported only with `llama.cpp` compatible models and `bert` models. bert is more performant and available independently of the LLM model.


### Transcriptions endpoint

Note: requires ffmpeg in the container image, which is currently not shipped due to licensing issues. We will prepare separated images with ffmpeg. (stay tuned!)

Download one of the models from https://huggingface.co/ggerganov/whisper.cpp/tree/main in the `models` folder, and create a YAML file for your model:

```yaml
name: whisper-1
backend: whisper
parameters:
  model: whisper-en
```

The transcriptions endpoint then can be tested like so:
```
wget --quiet --show-progress -O gb1.ogg https://upload.wikimedia.org/wikipedia/commons/1/1f/George_W_Bush_Columbia_FINAL.ogg

curl http://localhost:8080/v1/audio/transcriptions -H "Content-Type: multipart/form-data" -F file="@$PWD/gb1.ogg" -F model="whisper-1"                                                     

{"text":"My fellow Americans, this day has brought terrible news and great sadness to our country.At nine o'clock this morning, Mission Control in Houston lost contact with our Space ShuttleColumbia.A short time later, debris was seen falling from the skies above Texas.The Columbia's lost.There are no survivors.One board was a crew of seven.Colonel Rick Husband, Lieutenant Colonel Michael Anderson, Commander Laurel Clark, Captain DavidBrown, Commander William McCool, Dr. Kultna Shavla, and Elon Ramon, a colonel in the IsraeliAir Force.These men and women assumed great risk in the service to all humanity.In an age when spaceflight has come to seem almost routine, it is easy to overlook thedangers of travel by rocket and the difficulties of navigating the fierce outer atmosphere ofthe Earth.These astronauts knew the dangers, and they faced them willingly, knowing they had a highand noble purpose in life.Because of their courage and daring and idealism, we will miss them all the more.All Americans today are thinking as well of the families of these men and women who havebeen given this sudden shock and grief.You're not alone.Our entire nation agrees with you, and those you loved will always have the respect andgratitude of this country.The cause in which they died will continue.Mankind has led into the darkness beyond our world by the inspiration of discovery andthe longing to understand.Our journey into space will go on.In the skies today, we saw destruction and tragedy.As farther than we can see, there is comfort and hope.In the words of the prophet Isaiah, \"Lift your eyes and look to the heavens who createdall these, he who brings out the starry hosts one by one and calls them each by name.\"Because of his great power and mighty strength, not one of them is missing.The same creator who names the stars also knows the names of the seven souls we mourntoday.The crew of the shuttle Columbia did not return safely to Earth yet we can pray that all aresafely home.May God bless the grieving families and may God continue to bless America.[BLANK_AUDIO]"}
```

  
### Image generation

OpenAI docs: https://platform.openai.com/docs/api-reference/images/create

LocalAI supports generating images with Stable diffusion, running on CPU.

| mode=0                                                                                                                | mode=1 (winograd/sgemm)                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| ![test](https://github.com/go-skynet/LocalAI/assets/2420543/7145bdee-4134-45bb-84d4-f11cb08a5638)                      | ![b643343452981](https://github.com/go-skynet/LocalAI/assets/2420543/abf14de1-4f50-4715-aaa4-411d703a942a)          |
| ![b6441997879](https://github.com/go-skynet/LocalAI/assets/2420543/d50af51c-51b7-4f39-b6c2-bf04c403894c)              | ![winograd2](https://github.com/go-skynet/LocalAI/assets/2420543/1935a69a-ecce-4afc-a099-1ac28cb649b3)                |
| ![winograd](https://github.com/go-skynet/LocalAI/assets/2420543/1979a8c4-a70d-4602-95ed-642f382f6c6a)                | ![winograd3](https://github.com/go-skynet/LocalAI/assets/2420543/e6d184d4-5002-408f-b564-163986e1bdfb)                |


To generate an image you can send a POST request to the `/v1/images/generations` endpoint with the instruction as the request body:

```bash
# 512x512 is supported too
curl http://localhost:8080/v1/images/generations -H "Content-Type: application/json" -d '{
            "prompt": "A cute baby sea otter",
            "size": "256x256" 
          }'
```

Available additional parameters: `mode`, `step`.

Note: To set a negative prompt, you can split the prompt with `|`, for instance: `a cute baby sea otter|malformed`.

```bash
curl http://localhost:8080/v1/images/generations -H "Content-Type: application/json" -d '{
            "prompt": "floating hair, portrait, ((loli)), ((one girl)), cute face, hidden hands, asymmetrical bangs, beautiful detailed eyes, eye shadow, hair ornament, ribbons, bowties, buttons, pleated skirt, (((masterpiece))), ((best quality)), colorful|((part of the head)), ((((mutated hands and fingers)))), deformed, blurry, bad anatomy, disfigured, poorly drawn face, mutation, mutated, extra limb, ugly, poorly drawn hands, missing limb, blurry, floating limbs, disconnected limbs, malformed hands, blur, out of focus, long neck, long body, Octane renderer, lowres, bad anatomy, bad hands, text",
            "size": "256x256"
          }'
```

Note: image generator supports images up to 512x512. You can use other tools however to upscale the image, for instance: https://github.com/upscayl/upscayl.


#### Setup

Note: In order to use the `images/generation` endpoint, you need to build LocalAI with `GO_TAGS=stablediffusion`.

{{< tabs >}}
{{% tab name="Prepare the model in runtime" %}}

While the API is running, you can install the model by using the `/models/apply` endpoint and point it to the `stablediffusion` model in the [models-gallery](https://github.com/go-skynet/model-gallery#image-generation-stable-diffusion):
```bash
curl http://localhost:8080/models/apply -H "Content-Type: application/json" -d '{         
     "url": "github:go-skynet/model-gallery/stablediffusion.yaml"
   }'
```

{{% /tab %}}
{{% tab name="Automatically prepare the model before start" %}}

You can set the `PRELOAD_MODELS` environment variable:

```bash
PRELOAD_MODELS=[{"url": "github:go-skynet/model-gallery/stablediffusion.yaml"}]
```

or as arg:

```bash
local-ai --preload-models '[{"url": "github:go-skynet/model-gallery/stablediffusion.yaml"}]'
```

or in a YAML file:

```bash
local-ai --preload-models-config "/path/to/yaml"
```

YAML:
```yaml
- url: github:go-skynet/model-gallery/stablediffusion.yaml
```

{{% /tab %}}
{{% tab name="Install manually" %}}

1. Create a model file `stablediffusion.yaml` in the models folder:

```yaml
name: stablediffusion
backend: stablediffusion
asset_dir: stablediffusion_assets
```
2. Create a `stablediffusion_assets` directory inside your `models` directory
3. Download the ncnn assets from https://github.com/EdVince/Stable-Diffusion-NCNN#out-of-box and place them in `stablediffusion_assets`.

The models directory should look like the following:

```
models
├── stablediffusion_assets
│   ├── AutoencoderKL-256-256-fp16-opt.param
│   ├── AutoencoderKL-512-512-fp16-opt.param
│   ├── AutoencoderKL-base-fp16.param
│   ├── AutoencoderKL-encoder-512-512-fp16.bin
│   ├── AutoencoderKL-fp16.bin
│   ├── FrozenCLIPEmbedder-fp16.bin
│   ├── FrozenCLIPEmbedder-fp16.param
│   ├── log_sigmas.bin
│   ├── tmp-AutoencoderKL-encoder-256-256-fp16.param
│   ├── UNetModel-256-256-MHA-fp16-opt.param
│   ├── UNetModel-512-512-MHA-fp16-opt.param
│   ├── UNetModel-base-MHA-fp16.param
│   ├── UNetModel-MHA-fp16.bin
│   └── vocab.txt
└── stablediffusion.yaml
```


{{% /tab %}}

{{< /tabs >}}

## LocalAI API endpoints

Besides the OpenAI endpoints, there are additional LocalAI-only API endpoints.

Here is a table:

| Endpoint | Description |
| --- | --- |
| `/tts` | Text to Audio generation |
| `/models/apply` | Apply a model |
| `/models/jobs/:uid` | Apply a model |
| `/models/available` | Remove a model |

### Generate Audio from text - `/tts`

This endpoint can be used to generate speech from text.

Input: `input`, `model`

```bash
curl http://localhost:8080/tts -H "Content-Type: application/json" -d '{
            "input": "Hello world",
            "model": "tts"
          }'
```

Returns an `audio/wav` file.

#### Setup

To install audio models manually:

- Download Voices from https://github.com/rhasspy/piper/releases/tag/v0.0.2
- Extract the `.tar.tgz` files (.onnx,.json) into `models`
- Run the following command to test the model is working:

```bash
curl http://localhost:8080/tts -H "Content-Type: application/json" -d '{         
     "model":"it-riccardo_fasol-x-low.onnx",
     "input": "Ciao, sono Ettore"
   }' | aplay
```

Note: 
- `aplay` is a Linux command. You can use other tools to play the audio file.
- The model name is the filename with the extension.
- The model name is case sensitive.
- LocalAI must be compiled with the `GO_TAGS=tts` flag.

### Applying a model - `/models/apply`

This endpoint can be used to install a model in runtime. 

LocalAI will create a batch process that downloads the required files from a model definition and automatically reload itself to include the new model. 

Input: `url` or `id` (required), `name` (optional), `files` (optional)

```bash
curl http://localhost:8080/models/apply -H "Content-Type: application/json" -d '{
     "url": "<MODEL_DEFINITION_URL>",
     "id": "<GALLERY>@<MODEL_NAME>",
     "name": "<INSTALLED_MODEL_NAME>",
     "files": [
        {
            "uri": "<additional_file>",
            "sha256": "<additional_file_hash>",
            "filename": "<additional_file_name>"
        },
      "overrides": { "backend": "...", "f16": true }
     ]
   }
```

An optional, list of additional files can be specified to be downloaded within `files`. The `name` allows to override the model name. Finally it is possible to override the model config file with `override`.

The `url` is a full URL, or a github url (`github:org/repo/file.yaml`), or a local file (`file:///path/to/file.yaml`).
The `id` is a string in the form `<GALLERY>@<MODEL_NAME>`, where `<GALLERY>` is the name of the gallery, and `<MODEL_NAME>` is the name of the model in the gallery. Galleries can be specified during startup with the `GALLERIES` environment variable.

Returns an `uuid` and an `url` to follow up the state of the process:

```json
{ "uuid":"251475c9-f666-11ed-95e0-9a8a4480ac58", "status":"http://localhost:8080/models/jobs/251475c9-f666-11ed-95e0-9a8a4480ac58"}
```

To see a collection example of curated models definition files, see the [model-gallery](https://github.com/go-skynet/model-gallery).

### Get model job state `/models/jobs/<uid>`

This endpoint returns the state of the batch job associated to a model installation.

```bash
curl http://localhost:8080/models/jobs/<JOB_ID>
```

Returns a json containing the error, and if the job is being processed:

```json
{"error":null,"processed":true,"message":"completed"}
```

### List all available models - `/models/available`

To list all the available models, use the following endpoint:

```bash
curl http://localhost:8080/models/available
```

Returns a json containing the list of available models:

```json
[
  {
    "url": "github:go-skynet/model-gallery/virtual.yaml",
    "name": "voice-zh-cn-huayan-x-low",
    "license": "other",
    "urls": [
      "https://github.com/rhasspy/piper/releases/download/v0.0.2/"
    ],
    "files": [
      {
        "filename": "voice-zh-cn-huayan-x-low.tar.gz",
        "sha256": "",
        "uri": "https://github.com/rhasspy/piper/releases/download/v0.0.2/voice-zh-cn-huayan-x-low.tar.gz"
      }
    ],
    "gallery": {
      "url": "github:go-skynet/model-gallery/index.yaml",
      "name": "model-gallery"
    }
  },
  {
    "url": "github:go-skynet/model-gallery/virtual.yaml",
    "name": "voice-zh_CN-huayan-medium",
    "license": "other",
    "urls": [
      "https://github.com/rhasspy/piper/releases/download/v0.0.2/"
    ],
    "files": [
      {
        "filename": "voice-zh_CN-huayan-medium.tar.gz",
        "sha256": "",
        "uri": "https://github.com/rhasspy/piper/releases/download/v0.0.2/voice-zh_CN-huayan-medium.tar.gz"
      }
    ],
    "gallery": {
      "url": "github:go-skynet/model-gallery/index.yaml",
      "name": "model-gallery"
    }
  }
]
```

To install a model from one repository, we would use the `id` field, which is in the form `<GALLERY>@<MODEL_NAME>`. For example, to install the `voice-zh-cn-huayan-x-low` model from the `model-gallery` gallery, we would use the following command:

```bash
curl http://localhost:8080/models/apply -H "Content-Type: application/json" -d '{
     "id": "model-gallery@voice-zh-cn-huayan-x-low"
   }
```
