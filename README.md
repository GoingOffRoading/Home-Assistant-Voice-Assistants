# Home-Assistant-Voice-Assistant
I didn't see [documentation or examples of how to spin up local versions of Home Assistant local Voice Assistant](https://www.home-assistant.io/voice_control/), so I wanted to provide my notes on my own local control here.

# Basic Dependencies
Voice Assistants in Home Assistant need three component functions:
- Conversation Agent
- Speed to Text
- Text-to-speech
These services can run anywhere (Locally, Azure, GCP, AWS, etc) and just need to be accessible to your instance of Home Assistant.

## Conversation Agent