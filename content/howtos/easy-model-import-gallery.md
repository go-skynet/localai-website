
+++
disableToc = false
title = "Easy Model Import - Gallery"
weight = 2
+++

Now lets pick a model to download and test out. We are going to use `luna-ai-llama2-uncensored.Q4_K_M.gguf`, there are a few ways to do this, https://huggingface.co/TheBloke/Luna-AI-Llama2-Uncensored-GGUF/resolve/main/luna-ai-llama2-uncensored.Q4_K_M.gguf

The below command requires the Docker container already running,
and uses the Model Gallery to download the model.
it will set up a model YAML config file for you.

Run the following in a command line.

```bash
curl http://localhost:8080/models/apply -H "Content-Type: application/json" -d '{
     "id": "model-gallery@lunademo"
   }'  
```

Yes I know haha - ``Luna Midori`` making a how to using the ``luna-ai-llama2`` model - lol

In the `"lunademo.yaml"` file, fould in your models folder, edit it for your setup. (If you want to see advanced yaml configs - [Link](https://localai.io/advanced/))

If you are running on CPU only, remove the ``f16`` and ``gpu_layer`` lines from the yaml

Now that we have that fully set up, we need to reboot the Docker container. Go back to the localai folder and run

```bash
docker-compose restart
```

Now that we got that setup, lets test it out but sending a request by using [Curl]({{%relref "easy-request-curl" %}}) Or use the [Openai Python API]({{%relref "easy-request-openai" %}})! 
