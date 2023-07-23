
+++
disableToc = false
title = "🔥 OpenAI functions"
weight = 2
+++

LocalAI supports running OpenAI functions with `llama.cpp` compatible models.

![localai-functions-1](https://github.com/ggerganov/llama.cpp/assets/2420543/5bd15da2-78c1-4625-be90-1e938e6823f1)

To learn more about OpenAI functions, see the [OpenAI API blog post](https://openai.com/blog/function-calling-and-other-api-updates).

{{% notice note %}}
This feature is compatible only with the `llama-grammar` backend. A separate backend was created to track a specific `llama.cpp` branch as it depends on https://github.com/ggerganov/llama.cpp/pull/1773 which currently has not been merged yet. Once it will be merged it will be available in the `llama` backend.
{{% /notice %}}

## Setup

Specify the `llama-grammar` backend in the model YAML configuration file:

```yaml
name: openllama
parameters:
  model: ggml-openllama.bin
  top_p: 80
  top_k: 0.9
  temperature: 0.1
backend: llama-grammar # Set the `llama-grammar` backend
```

## Usage example

To use the functions with the OpenAI client in python:

```python
import openai
# ...
# Send the conversation and available functions to GPT
messages = [{"role": "user", "content": "What's the weather like in Boston?"}]
functions = [
    {
        "name": "get_current_weather",
        "description": "Get the current weather in a given location",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "The city and state, e.g. San Francisco, CA",
                },
                "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]},
            },
            "required": ["location"],
        },
    }
]
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=messages,
    functions=functions,
    function_call="auto",
)
# ...
```

{{% notice note %}}
When running the python script, be sure to:

- Set `OPENAI_API_KEY` environment variable to a random string (the OpenAI api key is NOT required!)
- Set `OPENAI_API_BASE` to point to your LocalAI service, for example `OPENAI_API_BASE=http://localhost:8080`

{{% /notice %}}


## 💡 Examples

A full e2e example with `docker-compose` is available here: https://github.com/go-skynet/LocalAI/tree/master/examples/functions
