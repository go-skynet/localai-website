
+++
disableToc = false
title = "Easy Request - Openai V1"
weight = 2
+++

This is for Python, ``OpenAI``=>``V1``, if you are on ``OpenAI``<``V1`` please use this [How to]({{%relref "howtos/easy-request-openai-v0" %}})

OpenAI Chat API Python -
```python
from openai import OpenAI

client = OpenAI(base_url="/v1", api_key="sk-xxx")

messages = [
{"role": "system", "content": "You are LocalAI, a helpful, but really confused ai, you will only reply with confused emotes"},
{"role": "user", "content": "Hello How are you today LocalAI"}
]
completion = client.chat.completions.create(
  model="gpt-3.5-turbo",
  messages=messages,
)

print(completion.choices[0].message)
```
