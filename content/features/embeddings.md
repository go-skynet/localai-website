
+++
disableToc = false
title = "🧠 Embeddings"
weight = 2
+++

OpenAI docs: https://platform.openai.com/docs/api-reference/embeddings

The embedding endpoint is experimental and enabled only if the model is configured with `embeddings: true` in its `yaml` file, for example:

```yaml
name: text-embedding-ada-002
parameters:
  model: bert
embeddings: true
backend: "bert-embeddings"
```

There is an example available [here](https://github.com/go-skynet/LocalAI/tree/master/examples/query_data/).

Note: embeddings is supported only with `llama.cpp` compatible models and `bert` models. bert is more performant and available independently of the LLM model.
