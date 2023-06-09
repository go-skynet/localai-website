
+++
disableToc = false
title = "Getting started"
weight = 2
+++

`LocalAI` is available as a container image and binary. You can check out all the available images with corresponding tags [here](https://quay.io/repository/go-skynet/local-ai?tab=tags&tag=latest).

The easiest way to run LocalAI is by using `docker-compose` (to build locally, see the [build section]({{%relref "basics/build" %}})):

```bash

git clone https://github.com/go-skynet/LocalAI

cd LocalAI

# (optional) Checkout a specific LocalAI tag
# git checkout -b build <TAG>

# copy your models to models/
cp your-model.bin models/

# (optional) Edit the .env file to set things like context size and threads
# vim .env

# start with docker-compose
docker-compose up -d --pull always
# or you can build the images with:
# docker-compose up -d --build

# Now API is accessible at localhost:8080
curl http://localhost:8080/v1/models
# {"object":"list","data":[{"id":"your-model.bin","object":"model"}]}

curl http://localhost:8080/v1/completions -H "Content-Type: application/json" -d '{
     "model": "your-model.bin",            
     "prompt": "A long time ago in a galaxy far, far away",
     "temperature": 0.7
   }'
```

### Example: Use GPT4ALL-J model with `docker-compose`


```bash
# Clone LocalAI
git clone https://github.com/go-skynet/LocalAI

cd LocalAI

# (optional) Checkout a specific LocalAI tag
# git checkout -b build <TAG>

# Download gpt4all-j to models/
wget https://gpt4all.io/models/ggml-gpt4all-j.bin -O models/ggml-gpt4all-j

# Use a template from the examples
cp -rf prompt-templates/ggml-gpt4all-j.tmpl models/

# (optional) Edit the .env file to set things like context size and threads
# vim .env

# start with docker-compose
docker-compose up -d --pull always
# or you can build the images with:
# docker-compose up -d --build
# Now API is accessible at localhost:8080
curl http://localhost:8080/v1/models
# {"object":"list","data":[{"id":"ggml-gpt4all-j","object":"model"}]}

curl http://localhost:8080/v1/chat/completions -H "Content-Type: application/json" -d '{
     "model": "ggml-gpt4all-j",
     "messages": [{"role": "user", "content": "How are you?"}],
     "temperature": 0.9 
   }'

# {"model":"ggml-gpt4all-j","choices":[{"message":{"role":"assistant","content":"I'm doing well, thanks. How about you?"}}]}
```

{{% notice note %}}
If running on Apple Silicon it is **not** suggested to run on Docker due to emulation. Follow the [build instructions]({{%relref "basics/build" %}}).
{{% /notice %}}

### From binaries

LocalAI binary releases are available in [Github](https://github.com/go-skynet/LocalAI/releases).

You can control LocalAI with command line arguments, to specify a binding address, or the number of threads.

<details>

Usage:

```
local-ai --models-path <model_path> [--address <address>] [--threads <num_threads>]
```

| Parameter                      | Environmental Variable          | Default Variable                                   | Description                                                         |
| ------------------------------ | ------------------------------- | -------------------------------------------------- | ------------------------------------------------------------------- |
| --f16                          | $F16                            | false                                              | Enable f16 mode                                                     |
| --debug                        | $DEBUG                          | false                                              | Enable debug mode                                                   |
| --cors                         | $CORS                           | false                                              | Enable CORS support                                                 |
| --cors-allow-origins value     | $CORS_ALLOW_ORIGINS             |                                                    | Specify origins allowed for CORS                                     |
| --threads value                | $THREADS                        | 4    | Number of threads to use for parallel computation                    |
| --models-path value            | $MODELS_PATH                    | ./models       | Path to the directory containing models used for inferencing        |
| --preload-models value         | $PRELOAD_MODELS                 |           | List of models to preload in JSON format at startup                  |
| --preload-models-config value  | $PRELOAD_MODELS_CONFIG          |  | A config with a list of models to apply at startup. Specify the path to a YAML config file |
| --config-file value            | $CONFIG_FILE                    |                                         | Path to the config file                                             |
| --address value                | $ADDRESS                        | :8080                    | Specify the bind address for the API server                         |
| --image-path value             | $IMAGE_PATH                     |                                     | Path to the directory used to store generated images                             |
| --context-size value           | $CONTEXT_SIZE                   | 512                 | Default context size of the model                                   |
| --upload-limit value           | $UPLOAD_LIMIT                   | 15                         | Default upload limit in megabytes (audio file upload)                                  |

</details>

### Docker

LocalAI has a set of images to support CUDA, ffmpeg and 'vanilla' (CPU-only). The image list is on [quay](https://quay.io/repository/go-skynet/local-ai?tab=tags):

- Vanilla images tags: `master`, `v1.18.0`, ...
- FFmpeg images tags: `master-ffmpeg`, `v1.18.0-ffmpeg`, ...
- CUDA `11` tags: `master-cublas-cuda11`, `v1.18.0-cublas-cuda11`, ...
- CUDA `12` tags: `master-cublas-cuda12`, `v1.18.0-cublas-cuda12`, ...
- CUDA `11` + FFmpeg tags: `master-cublas-cuda11-ffmpeg`, `v1.18.0-cublas-cuda11-ffmpeg`, ...
- CUDA `12` + FFmpeg tags: `master-cublas-cuda12-ffmpeg`, `v1.18.0-cublas-cuda12-ffmpeg`, ...

<details>
Example of starting the API with `docker`:

```bash
docker run -p 8080:8080 -ti --rm quay.io/go-skynet/local-ai:latest --models-path /path/to/models --context-size 700 --threads 4
```

You should see:
```
┌───────────────────────────────────────────────────┐ 
│                   Fiber v2.42.0                   │ 
│               http://127.0.0.1:8080               │ 
│       (bound on host 0.0.0.0 and port 8080)       │ 
│                                                   │ 
│ Handlers ............. 1  Processes ........... 1 │ 
│ Prefork ....... Disabled  PID ................. 1 │ 
└───────────────────────────────────────────────────┘ 
```

{{% notice note %}}
Note: the binary inside the image is rebuild at the start of the container to enable CPU optimizations for the execution environment, you can set the environment variable `REBUILD` to `false` to prevent this behavior.
{{% /notice %}}

</details>


### Run LocalAI in Kubernetes

LocalAI can be installed inside Kubernetes with helm.

<details>
By default, the helm chart will install LocalAI instance using the ggml-gpt4all-j model without persistent storage.

1. Add the helm repo
    ```bash
    helm repo add go-skynet https://go-skynet.github.io/helm-charts/
    ```
2. Install the helm chart:
    ```bash
    helm repo update
    helm install local-ai go-skynet/local-ai -f values.yaml
    ```
> **Note:** For further configuration options, see the [helm chart repository on GitHub](https://github.com/go-skynet/helm-charts).
### Example values
Deploy a single LocalAI pod with 6GB of persistent storage serving up a `ggml-gpt4all-j` model with custom prompt.
```yaml
### values.yaml

deployment:
  # Adjust the number of threads and context size for model inference
  env:
    threads: 4
    contextSize: 512

# Set the pod requests/limits
resources:
  limits:
    cpu: 4000m
    memory: 7000Mi
  requests:
    cpu: 100m
    memory: 6000Mi

# Add a custom prompt template for the ggml-gpt4all-j model
promptTemplates:
  # The name of the model this template belongs to
  ggml-gpt4all-j.bin.tmpl: |
    This is my custom prompt template...
    ### Prompt:
    {{.Input}}
    ### Response:

# Model configuration
models:
  # Don't re-download models on pod creation
  forceDownload: false

  # List of models to download and serve
  list:
    - url: "https://gpt4all.io/models/ggml-gpt4all-j.bin"
       # Optional basic HTTP authentication
      basicAuth: base64EncodedCredentials
  
  # Enable 6Gb of persistent storage models and prompt templates
  persistence:
    enabled: true
    size: 6Gi

service:
  type: ClusterIP
  annotations: {}
  # If using an AWS load balancer, you'll need to override the default 60s load balancer idle timeout
  # service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout: "1200"
```
</details>


### Build from source

See the [build section]({{%relref "basics/build" %}}).

### Other examples

![Screenshot from 2023-04-26 23-59-55](https://user-images.githubusercontent.com/2420543/234715439-98d12e03-d3ce-4f94-ab54-2b256808e05e.png)

To see other examples on how to integrate with other projects for instance for question answering or for using it with chatbot-ui, see: [examples](https://github.com/go-skynet/LocalAI/tree/master/examples/).