
+++
disableToc = false
title = "Getting started"
weight = 2
+++

`LocalAI` comes by default as a container image. You can check out all the available images with corresponding tags [here](https://quay.io/repository/go-skynet/local-ai?tab=tags&tag=latest).

The easiest way to run LocalAI is by using `docker-compose` (to build locally, see [building LocalAI](https://github.com/go-skynet/LocalAI/tree/master#setup)):

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


### From binaries

LocalAI binary releases are available in [Github](https://github.com/go-skynet/LocalAI/releases).

You can control LocalAI with command line arguments, to specify a binding address, or the number of threads.

<details>

Usage:

```
local-ai --models-path <model_path> [--address <address>] [--threads <num_threads>]
```

| Parameter    | Environment Variable | Default Value | Description                            |
| ------------ | -------------------- | ------------- | -------------------------------------- |
| models-path        | MODELS_PATH           |               | The path where you have models (ending with `.bin`).      |
| threads      | THREADS              | Number of Physical cores     | The number of threads to use for text generation. |
| address      | ADDRESS              | :8080         | The address and port to listen on. |
| context-size | CONTEXT_SIZE         | 512           | Default token context size. |
| debug | DEBUG         | false           | Enable debug mode. |
| config-file | CONFIG_FILE         | empty           | Path to a LocalAI config file. |
| upload_limit | UPLOAD_LIMIT         | 5MB           | Upload limit for whisper. |
| image-path | IMAGE_PATH         | empty           | Image directory to store and serve processed images. |

</details>

### Docker

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

Note: the binary inside the image is rebuild at the start of the container to enable CPU optimizations for the execution environment, you can set the environment variable `REBUILD` to `false` to prevent this behavior.

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
    threads: 14
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

See the [build section]



</details>

### Other examples

![Screenshot from 2023-04-26 23-59-55](https://user-images.githubusercontent.com/2420543/234715439-98d12e03-d3ce-4f94-ab54-2b256808e05e.png)

To see other examples on how to integrate with other projects for instance for question answering or for using it with chatbot-ui, see: [examples](https://github.com/go-skynet/LocalAI/tree/master/examples/).