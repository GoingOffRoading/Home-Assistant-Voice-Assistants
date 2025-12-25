# Home-Assistant-Voice-Assistant
I didn't see [documentation or examples of how to spin up local versions of Home Assistant local Voice Assistant](https://www.home-assistant.io/voice_control/), so I wanted to provide my notes on my own local control here.

# Basic Dependencies
Voice Assistants in Home Assistant need three component functions:
- Conversation Agent
- Speed to Text
- Text-to-speech
These services can run anywhere (Locally, Azure, GCP, AWS, etc) and just need to be accessible to your instance of Home Assistant.

## Conversation Agent
For this, I recommend [Olamma](https://docs.ollama.com/docker).  Ollama is a self-hostable platform for hosting and running Large Language Models (LLMs).  It also has [a direct integration with Home Assistant](https://www.home-assistant.io/integrations/ollama/). 

## Speed to Text
For this, I recommend [Fast-Whisper or 'Whisper' for short](https://docs.linuxserver.io/images/docker-faster-whisper/).  Whisper is a self-hostable OpenAI open sourced tool for  for hosting and running speech to text.  Like Olamma, it also has [a direct integration with Home Assistant](https://www.home-assistant.io/integrations/whisper/). 