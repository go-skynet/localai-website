
+++
disableToc = false
title = "Build"
weight = 3
+++

### Build locally

<details>

In order to build the `LocalAI` container image locally you can use `docker`:

```
# build the image
docker build -t LocalAI .
docker run LocalAI
```

Or you can build the binary with `make`:

```
make build
```

</details>

### Build on mac

Building on Mac (M1 or M2) works, but you may need to install some prerequisites using `brew`. 

<details>

The below has been tested by one mac user and found to work. Note that this doesn't use docker to run the server:

```
# install build dependencies
brew install cmake
brew install go

# clone the repo
git clone https://github.com/go-skynet/LocalAI.git

cd LocalAI

# build the binary
make build

# Download gpt4all-j to models/
wget https://gpt4all.io/models/ggml-gpt4all-j.bin -O models/ggml-gpt4all-j

# Use a template from the examples
cp -rf prompt-templates/ggml-gpt4all-j.tmpl models/

# Run LocalAI
./local-ai --models-path ./models/ --debug

# Now API is accessible at localhost:8080
curl http://localhost:8080/v1/models

curl http://localhost:8080/v1/chat/completions -H "Content-Type: application/json" -d '{
     "model": "ggml-gpt4all-j",
     "messages": [{"role": "user", "content": "How are you?"}],
     "temperature": 0.9 
   }'
```

</details>

### Build with Image generation support

<details>

**Requirements**: OpenCV, Gomp

Image generation is experimental and requires `GO_TAGS=stablediffusion` to be set during build:

```
make GO_TAGS=stablediffusion rebuild
```

</details>

### Accelleration

#### OpenBLAS

<details>

Requirements: OpenBLAS

```
make BUILD_TYPE=openblas build
```

</details>

#### CuBLAS

<details>

Requirement: Nvidia CUDA toolkit

Note: CuBLAS support is experimental, and has not been tested on real HW. please report any issues you find!

```
make BUILD_TYPE=cublas build
```

More informations available in the upstream PR: https://github.com/ggerganov/llama.cpp/pull/1412

</details>

### Windows compatibility

It should work, however you need to make sure you give enough resources to the container. See https://github.com/go-skynet/LocalAI/issues/2