---
categories: ["Examples"]
tags: ["docs"] 
title: "Getting Started"
linkTitle: "Getting Started"
weight: 3
description: >
  This page will help you get started with LocalAI.
---

{{% pageinfo %}}
This page will help you get started with LocalAI. You can edit the content of this page by clicking on the `Edit this page` button in the top right corner.
{{% /pageinfo %}}


## Prerequisites

* Docker
* Go 1.19+
* Open-source models


## Installation

```bash
git clone https://github.com/go-skynet/LocalAI

cd LocalAI

```bash

# Download gpt4all-j to models/
wget https://gpt4all.io/models/ggml-gpt4all-j.bin -O models/ggml-gpt4all-j

# Use a template from the examples
cp -rf prompt-templates/ggml-gpt4all-j.tmpl models/

# (optional) Edit the .env file to set things like context size and threads
# vim .env
```

Currently LocalAI comes as a container image and can be used with docker or a container engine of choice. You can check out all the available images with corresponding tags [here](https://quay.io/repository/go-skynet/local-ai?tab=tags&tag=latest).



## Start the API

```bash
# start with docker-compose
docker-compose up -d --pull always

# You should see something like this:
┌───────────────────────────────────────────────────┐ 
│                   Fiber v2.42.0                   │ 
│               http://127.0.0.1:8080               │ 
│       (bound on host 0.0.0.0 and port 8080)       │ 
│                                                   │ 
│ Handlers ............. 1  Processes ........... 1 │ 
│ Prefork ....... Disabled  PID ................. 1 │ 
└───────────────────────────────────────────────────┘ 


# Now API is accessible at localhost:8080
curl http://localhost:8080/v1/models
# {"object":"list","data":[{"id":"ggml-gpt4all-j","object":"model"}]}
```

## Try it out!
```bash
curl http://localhost:8080/v1/chat/completions -H "Content-Type: application/json" -d '{
     "model": "ggml-gpt4all-j",
     "messages": [{"role": "user", "content": "How are you?"}],
     "temperature": 0.9 
   }'

# {"model":"ggml-gpt4all-j","choices":[{"message":{"role":"assistant","content":"I'm doing well, thanks. How about you?"}}]}
```
