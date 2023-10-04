
+++
disableToc = false
title = "Easy Model Import - Gallery"
weight = 2
+++

Now lets pick a model to download and test out. We are going to use `luna-ai-llama2-uncensored.Q4_0.gguf`, there are a few ways to do this, https://huggingface.co/TheBloke/Luna-AI-Llama2-Uncensored-GGUF/resolve/main/luna-ai-llama2-uncensored.Q4_0.gguf

The below command requires the Docker container already running,
and uses the Model Gallery to download the model.
it may also set up a model YAML config file,
but we will need to override that for this how to setup!

```bash
curl --location 'http://localhost:8080/models/apply' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "TheBloke/Luna-AI-Llama2-Uncensored-GGUF/luna-ai-llama2-uncensored.Q4_0.gguf",
    "name": "lunademo"
}'
```

Yes I know haha - ``Luna Midori`` making a how to using the ``luna-ai-llama2`` model - lol

{{% notice note %}}
You will need to delete the following 3 files that hugging face downloaded...

- chat.tmpl
- completion.tmpl
- lunademo.yaml
{{% /notice %}}

Now lets make 3 files in the models folder. 

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
backend: llama
context_size: 2000
f16: true ## If you are using cpu set this to false
gpu_layers: 4
name: lunademo
parameters:
  model: luna-ai-llama2-uncensored.Q4_0.gguf
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

Now that we have that fully set up, we need to reboot the Docker container. Go back to the localai folder and run

```bash
docker-compose restart
```

Now that we got that setup, lets test it out but sending a request by using [Curl]({{%relref "easy-request-curl" %}}) Or use the [Openai Python API]({{%relref "easy-request-openai" %}})! 
