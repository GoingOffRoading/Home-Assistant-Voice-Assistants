# Home-Assistant-Voice-Assistant
I didn't see [examples of how to spin up local versions of Home Assistant local Voice Assistant](https://www.home-assistant.io/voice_control/) nor in the [Getting Started-Local](https://www.home-assistant.io/voice_control/voice_remote_local_assistant/), so I wanted to provide my notes on my own 100% local control here.

# Basic Dependencies
Voice Assistants in Home Assistant need three component functions:
- Conversation Agent
- Speech-to-Text
- Text-to-Speech
These services can run anywhere (Locally, Azure, GCP, AWS, etc) and just need to be accessible to your instance of Home Assistant.

## Conversation Agent
For this, I recommend [Olamma](https://docs.ollama.com/docker).  Ollama is a self-hostable platform for hosting and running Large Language Models (LLMs).  It also has [a direct integration with Home Assistant](https://www.home-assistant.io/integrations/ollama/). 

## Speech-to-Text
For this, I recommend [Fast-Whisper or 'Whisper' for short](https://docs.linuxserver.io/images/docker-faster-whisper/).  Whisper is a self-hostable OpenAI open sourced tool for  for hosting and running speech to text.  Like Olamma, it also has [a direct integration with Home Assistant](https://www.home-assistant.io/integrations/whisper/). 

## Text-to-Speech
For this, I recommend [Piper](https://github.com/rhasspy/wyoming-piper).  Piper is a self-hostable tool for  for hosting and running text to speech.  Like Olamma and Whsiper, it also has [a direct integration with Home Assistant](https://www.home-assistant.io/integrations/piper/). 

# Configurating Home Assistant

Is reasonably well documented in the [Getting Started-Local](https://www.home-assistant.io/voice_control/voice_remote_local_assistant/).

What I wish was in the documentation:

## Ollama

- Download the model in advance.  Any of the models that fit the memory footprint of your machine AND are 'tool' compatible should suffice.  I am running llama3.2.

i.e. SSH into the Ollama container and run 'ollama pull llama3.2:latest'
