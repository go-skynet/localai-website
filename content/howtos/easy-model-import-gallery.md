
+++
disableToc = false
title = "Easy Model Import - Gallery"
weight = 2
+++

Now lets pick a model to test out. We are going to use `lunademo` from the gallery api

The below command requires the Docker container already running,
and uses the Model Gallery to download the model.
it will set up a model YAML config file for you.

Run the following in a command line.
```bash
curl http://localhost:8080/models/apply -H "Content-Type: application/json" -d '{
     "id": "model-gallery@lunademo"
   }'  
```

If you would like to add other models with out setting up the yaml or temp files. You may run
```bash
curl --location 'http://localhost:8080/models/apply' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": "NAME_OFF_HUGGINGFACE/REPO_NAME/MODENAME.gguf",
    "name": "REQUSTNAME"
}'
```

Yes I know haha - ``Luna Midori`` making a how to using the ``luna-ai-llama2`` model - lol

In the `"lunademo.yaml"` file, fould in your models folder, edit it for your setup. (If you want to see advanced yaml configs - [Link](https://localai.io/advanced/))

If you are running on CPU only, remove the ``f16`` and ``gpu_layer`` lines from the yaml that was made in your ``models`` folder by the gallery api. You can edit the number of ``gpu_layer`` for your gpu (IE a 4090 has 12gb vram, so you can set ``gpu_layer`` to 35 for this model).


Now that we have that fully set up, we need to reboot the Docker container. Go back to the localai folder and run

```bash
docker-compose restart
```

Now that we got that setup, lets test it out but sending a request by using [Curl]({{%relref "easy-request-curl" %}}) Or use the [Openai Python API]({{%relref "easy-request-openai" %}})! 
