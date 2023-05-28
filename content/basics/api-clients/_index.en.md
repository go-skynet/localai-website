

+++
disableToc = false
title = "API Clients"
weight = 4
+++


## Clients

OpenAI clients are already compatible with LocalAI by overriding the basePath, or the target URL.

## Javascript

<details> 

https://github.com/openai/openai-node/

```javascript
import { Configuration, OpenAIApi } from 'openai';

const configuration = new Configuration({
  basePath: `http://localhost:8080/v1`
});
const openai = new OpenAIApi(configuration);
```

</details>

## Python

<details>

https://github.com/openai/openai-python

Set the `OPENAI_API_BASE` environment variable, or by code:

```python
import openai

openai.api_base = "http://localhost:8080/v1"

# create a chat completion
chat_completion = openai.ChatCompletion.create(model="gpt-3.5-turbo", messages=[{"role": "user", "content": "Hello world"}])

# print the completion
print(completion.choices[0].message.content)
```

</details>