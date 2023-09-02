
+++
disableToc = false
title = "Easy Model Import - Gallery"
weight = 2
+++

Now lets pick a model to download and test out. We are going to use `llama-2-13b-chat.ggmlv3.q4_0.bin`, there are a few ways to do this, https://huggingface.co/TheBloke/Llama-2-13B-chat-GGML/blob/main/

In the `docker` cmd run this. This uses the Gallery to download the model, it may also set up the yaml file, but we will need to override that for the how to setup!
```bash
curl --location 'http://localhost:8080/models/apply' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "TheBloke/Llama-2-13B-chat-GGML/llama-2-13b-chat.ggmlv3.q4_0.bin",
    "name": "lunademo"
}'
```

Now lets make 3 files. (You may delete or edit if the gallery already made them)

```bash
touch lunademo-chat.tmpl
touch lunademo-completion.tmpl
touch lunademo.yaml
```

Please note the names for later!

In the `"lunademo-chat.tmpl"` file add

```txt
{{.Input}}

### Response:
```

In the `"lunademo-completion.tmpl"` file add

```txt
Complete the following sentence: {{.Input}}
```


In the `"lunademo.yaml"` file (If you want to see advanced yaml configs - [Link](https://localai.io/advanced/))

```yaml
backend: llama-stable
context_size: 2000
gpu_layers: 4
batch: 512
name: lunademo
parameters:
  model: llama-2-13b-chat.ggmlv3.q4_0.bin
  temperature: 0.2
  top_k: 40
  top_p: 0.65
roles:
  assistant: '### Response:'
  system: '### System:'
  user: '### Instruction:'
template:
  chat: lunademo-chat
  completion: lunademo-completion
```

Now that we have that fully set up, we need to reboot the docker. Go back to the localai folder and run

```bash
docker-compose restart
```

Now that we got that setup, lets test it out but sending a request by using [Curl]({{%relref "easy-request-curl" %}}) Or use the [Openai Python API]({{%relref "easy-request-openai" %}})! 
