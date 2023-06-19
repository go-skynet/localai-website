
+++
disableToc = false
title = "FAQ"
weight = 5
+++

## Frequently asked questions

Here are answers to some of the most common questions.


### How do I get models? 

<details>

Most ggml-based models should work, but newer models may require additions to the API. If a model doesn't work, please feel free to open up issues. However, be cautious about downloading models from the internet and directly onto your machine, as there may be security vulnerabilities in lama.cpp or ggml that could be maliciously exploited. Some models can be found on Hugging Face: https://huggingface.co/models?search=ggml, or models from gpt4all are compatible too: https://github.com/nomic-ai/gpt4all.

</details>

### What's the difference with Serge, or XXX?


<details>

LocalAI is a multi-model solution that doesn't focus on a specific model type (e.g., llama.cpp or alpaca.cpp), and it handles all of these internally for faster inference,  easy to set up locally and deploy to Kubernetes.

</details>


### Everything is slow, how come?

<details>

There are few situation why this could occur. Some tips are:
- Don't use HDD to store your models. Prefer SSD over HDD. In case you are stuck with HDD, disable `mmap` in the model config file so it loads everything in memory.
- Watch out CPU overbooking. Ideally the `--threads` should match the number of physical cores. For instance if your CPU has 4 cores, you would ideally allocate `<= 4` threads to a model.
- Run LocalAI with `DEBUG=true`. This gives more information, including stats on the token inference speed.

</details>

### Can I use it with a Discord bot, or XXX?

<details>

Yes! If the client uses OpenAI and supports setting a different base URL to send requests to, you can use the LocalAI endpoint. This allows to use this with every application that was supposed to work with OpenAI, but without changing the application!

</details>


### Can this leverage GPUs? 

<details>

There is partial GPU support, see build instructions above.

</details>

### Where is the webUI? 

<details> 
There is the availability of localai-webui and chatbot-ui in the examples section and can be setup as per the instructions. However as LocalAI is an API you can already plug it into existing projects that provides are UI interfaces to OpenAI's APIs. There are several already on github, and should be compatible with LocalAI already (as it mimics the OpenAI API)

</details>

### Does it work with AutoGPT? 

<details>

Yes, see the [examples](https://github.com/go-skynet/LocalAI/tree/master/examples/)!

</details>