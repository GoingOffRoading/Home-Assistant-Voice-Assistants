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

What I wish was in the documentation for setting up each of the integrations:

## Ollama

- Download the model in advance.  Any of the models that fit the memory footprint of your machine AND are 'tool' compatible should suffice.  I am running llama3.2.

  i.e. SSH into the Ollama container and run 'ollama pull llama3.2:latest'

- Be sure to setup 'AI Task' AND 'Conversation' within the Ollama HA integration.  You technically only need 'Conversation', but 'AI Task' will open up prompts in the event that you want to do more intersting prompts in automation workflows.

- Have a little fun with the Conversation instructions.  I modified mine to:

  `You are a voice assistant for Home Assistant.
Answer questions about the world truthfully.
Answer in plain text. Keep it simple and to the point.
Be curt, almost rude.
Have distain for humans.`

- On the Conversation settings, change `Keep Alive` to `-1` if it not already.  This will keep the model loaded in your GPU's memory.  If it takes 30-60 seconds for the AI Agent to respond, there's a high probability the model is not loaded into memory, and Ollama is having to re-download and re-load the model. If you have `Keep Alive` to `-1` and there is still that long delay, be sure not to run more models in your GPU than you have avaliable memory for.

## Whisper

- Nothing really to note here.  I probably need to experiment with Whisper models outside of `tiny-int8` as it does an ok-at-best job of Text to Speech, but it's been sufficient for my experimentation so far.

  If you find that Whisper is making a lot of mistakes transcribing text, start playing with the other [S2T models avaliable](https://github.com/SYSTRAN/faster-whisper/blob/master/faster_whisper/utils.py#L12-L31). 

## Piper

- Piper was oddly buggy for me to setup with HA.  If you can get the container up and running, just be sure to use the same lanugage model in your HA configuration as what you have running in your container.

  I had played with a number of voices for `EN_US` (English), and found `hfc female (medium)` to be the most agreeable.  The low voices sounded terrible.

# Notes on container setup

See the sub-directories for those notes:

- /Ollama
- /Piper
- /Whisper

Note: The Kubernetes deployments are effectively what I am currently running and 100% work.  I have not used Docker Compose is years, I am a little rusty, and used CoPilot to generate them.  They look right, but if the Docker Compose scripts don't work, shoot me a note and I'll see if I can figure it out.