
+++
disableToc = false
title = "🆕 🦙 Exllama"
weight = 2
+++


[Exllama](https://github.com/turboderp/exllama) is a "A more memory-efficient rewrite of the HF transformers implementation of Llama for use with quantized weights"

## Setup

This is an extra backend - in the container is already available and there is nothing to do for the setup.


## Model setup

Download the model as a folder inside the `model ` directory and create a YAML file specifying the `exllama` backend. For instance with the `TheBloke/WizardLM-7B-uncensored-GPTQ` model:

```
$ git lfs install
$ cd models && git clone https://huggingface.co/TheBloke/WizardLM-7B-uncensored-GPTQ
$ ls models/                                                                 
.keep                        WizardLM-7B-uncensored-GPTQ/ exllama.yaml
$ cat models/exllama.yaml                                                     
name: exllama
parameters:
  model: WizardLM-7B-uncensored-GPTQ
backend: exllama
# ...
```

Test with:

```bash
curl http://localhost:8080/v1/chat/completions -H "Content-Type: application/json" -d '{                                                                                                         
   "model": "exllama",
   "messages": [{"role": "user", "content": "How are you?"}],
   "temperature": 0.1
 }'
```