
+++
disableToc = false
title = "Easy Model Import - Downloaded"
weight = 2
+++

Now lets pick a model to download and test out. We are going to use `luna-ai-llama2-uncensored.ggmlv3.q5_K_M.bin`, there are a few ways to do this, 

Now lets download and move the model.

Link - https://huggingface.co/TheBloke/Luna-AI-Llama2-Uncensored-GGML/blob/main/luna-ai-llama2-uncensored.ggmlv3.q5_K_M.bin

Using that link download the `luna-ai-llama2-uncensored.ggmlv3.q5_K_M.bin` model, once done, move the model.bin into the models folder.

Yes I know haha - ``Luna Midori`` making a how to using the ``luna-ai-llama2`` model - lol

Now lets make 3 files.

```bash
touch lunademo-chat.tmpl
touch lunademo-completion.tmpl
touch lunademo.yaml
```
Please note the names for later!

In the `"lunademo-chat.tmpl"` file add

```txt
{{.Input}}

ASSISTANT:
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
  model: luna-ai-llama2-uncensored.ggmlv3.q5_K_M.bin
  temperature: 0.2
  top_k: 40
  top_p: 0.65
roles:
  assistant: 'ASSISTANT:'
  system: 'SYSTEM:'
  user: 'USER:'
template:
  chat: lunademo-chat
  completion: lunademo-completion
```

Now that we have that fully set up, we need to reboot the docker. Go back to the localai folder and run

```bash
docker-compose restart
```

Now that we got that setup, lets test it out but sending a request by using [Curl]({{%relref "easy-request-curl" %}}) Or use the [Openai Python API]({{%relref "easy-request-openai" %}})! 
