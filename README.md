# Frontier Model APIs

This repository provides examples for connecting to and using APIs from leading large language models (LLMs), including OpenAI, Anthropic, Google Gemini, and DeepSeek. It demonstrates how to interact with various models, stream responses, and compare output across providers.

## Features

- Environment-based API key management
- API integrations:
  - **OpenAI** (`gpt-4o-mini`, `gpt-4.1`, `o3-mini`, etc.)
  - **Anthropic** (`claude-3-7-sonnet`, `claude-3-haiku`)
  - **Google Gemini** (`gemini-2.0-flash`, `gemini-2.5-flash-preview`)
  - **DeepSeek** (`deepseek-chat`, `deepseek-reasoner`)
- Temperature control for response randomness
- Streaming support (OpenAI, Claude, DeepSeek)
- Comparison between reasoning vs. casual models
- Conversational simulation between models (e.g. GPT vs Claude)

## Setup

1. Clone the repository.
2. Create a `.env` file in the root directory with the following content:

   ```env
   OPENAI_API_KEY=your_openai_key
   ANTHROPIC_API_KEY=your_anthropic_key
   GOOGLE_API_KEY=your_google_key
   DEEPSEEK_API_KEY=your_deepseek_key
   ```

3. Install dependencies:
```bash
pip install openai anthropic google-generativeai python-dotenv
```
## Usage
Basic Prompt Format
All models receive messages in this format:
```bash
pythonprompts = [
    {"role": "system", "content": "You are an assistant that is great at telling jokes"},
    {"role": "user", "content": "Tell a light-hearted joke for an audience of Data Scientists"}
]
```
## Example: OpenAI GPT-4o-mini
```bash
completion = openai.chat.completions.create(
    model='gpt-4o-mini',
    messages=prompts
)
print(completion.choices[0].message.content)
```
## and also Example: Anthropic Claude 3.7 Sonnet, Google Gemini, DeepSeek

## Streaming Responses
Most providers support streaming. Example with OpenAI:
```bash
stream = openai.chat.completions.create(
    model='gpt-4o-mini',
    messages=prompts,
    stream=True
)
for chunk in stream:
    print(chunk.choices[0].delta.content or '', end='', flush=True)
```

## Simulating Multi-Model Conversations
The script includes a simulated conversation between an argumentative GPT-4o-mini and a polite Claude-3-haiku. This helps explore the personality and reasoning differences between models.

## Notes
- API keys must be set properly for each model to work.

- Some models (e.g., Gemini) offer both official SDK and OpenAI-compatible endpoints.

- DeepSeek models may require special handling for streaming and reasoning content.
