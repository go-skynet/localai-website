
+++
disableToc = false
title = "🗣 Text to audio (TTS)"
weight = 2
+++

The `/tts` endpoint can be used to generate speech from text.

Input: `input`, `model`

For example, to generate an audio file, you can send a POST request to the `/tts` endpoint with the instruction as the request body:

```bash
curl http://localhost:8080/tts -H "Content-Type: application/json" -d '{
  "input": "Hello world",
  "model": "tts"
}'
```

Returns an `audio/wav` file.

#### Setup

To install audio models manually:

- Download Voices from https://github.com/rhasspy/piper/releases/tag/v0.0.2
- Extract the `.tar.tgz` files (.onnx,.json) into `models`
- Run the following command to test the model is working:

```bash
curl http://localhost:8080/tts -H "Content-Type: application/json" -d '{
  "model":"it-riccardo_fasol-x-low.onnx",
  "input": "Ciao, sono Ettore"
}' | aplay
```

Note:

- `aplay` is a Linux command. You can use other tools to play the audio file.
- The model name is the filename with the extension.
- The model name is case sensitive.
- LocalAI must be compiled with the `GO_TAGS=tts` flag.
