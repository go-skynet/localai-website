
+++
disableToc = false
title = "Easy Request - Openai"
weight = 2
+++

Now we can make a openai request!

OpenAI Chat API Python -

```python
import os
import openai
openai.api_base = "http://localhost:8080/v1"
openai.api_key = "sx-xxx"
OPENAI_API_KEY = "sx-xxx"
os.environ['OPENAI_API_KEY'] = OPENAI_API_KEY

completion = openai.ChatCompletion.create(
  model="lunademo",
  messages=[
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "How are you?"}
  ]
)

print(completion.choices[0].message)
```

OpenAI Completion API Python -

```python
import os
import openai
openai.api_base = "http://localhost:8080/v1"
openai.api_key = "sx-xxx"
OPENAI_API_KEY = "sx-xxx"
os.environ['OPENAI_API_KEY'] = OPENAI_API_KEY

completion = openai.ChatCompletion.create(
  model="lunademo",
  messages=[
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "How are you?"}
  ]
)

print(completion.choices[0].message)
```

Have fun using LocalAI!
