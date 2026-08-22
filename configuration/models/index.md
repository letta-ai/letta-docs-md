---
title: Models | Letta Docs
description: Configure models, providers, and reasoning settings in the Letta app or CLI
---

Letta agents are **model-agnostic**. Agents can use Claude, GPT, Gemini, or other supported models. Users can change an agent’s underlying model at any time, even mid-conversation.

We recommend first-time users use a large frontier model (for example from OpenAI or Anthropic) to learn how Letta agents work, since weaker models can cause the agent to behave in unexpected ways. See [leaderboard.letta.com](https://leaderboard.letta.com) for benchmarks comparing model performance.

## Switching models

Use the `/model` command to switch models during a session. This opens a model selector that allows you to swap models and choose their reasoning settings (if applicable).

## Model toolsets

Different models are trained to work best with different tools. For example, GPT models from OpenAI are trained to use a patch-based editing tool, while Claude models work better with string-based edit tools.

The Letta agent harness handles this automatically with dynamic **toolsets** - tool configurations optimized for each model family. When you switch models with `/model`, the toolset switches automatically. If you want to force a specific toolset, use the `/toolset` command.

Agents hosted in Letta Cloud come pre-configured with web search and web fetch tools. If you’re running agents using the local backend, you can set up your own web search utilities using custom [skills](/configuration/skills/index.md).

## Connecting model providers

The Letta app and CLI support a wide variety of LLM providers, as well as coding plans such as ChatGPT and zAI. To connect additional providers, use `/connect` in the CLI. To see your available models, use `/model`.

Local providers are configured on your machine. When you sign in with Letta, `/connect` also lets you configure providers for agents backed up to the cloud.

Cloud providers are managed through Letta’s LLM gateway. The gateway supports a smaller provider set than local setup; direct integrations with local inference providers such as LM Studio, Ollama, and llama.cpp are available only for local agents. You can pay for LLM gateway usage with pay-as-you-go credits from the [usage page](https://platform.letta.com/settings/organization/usage).

## Local models

There are two ways to use your own locally hosted models with Letta agents:

1. **Run the agent and model locally.** Use [local setup](/self-hosting/index.md), open `/connect`, and choose the built-in Ollama or LM Studio provider. Both the agent state and model endpoint remain on your machine.
2. **Connect a cloud-hosted agent to your model.** Open `/connect`, add an OpenAI-compatible API custom provider, and enter the base URL and API key for your inference server. Because the agent runs in the cloud, the endpoint must be reachable from the public internet rather than only through `localhost`. Use a stable public URL or static IP, secure it with authentication and HTTPS, and restrict access where possible.

The OpenAI-compatible endpoint must support Chat Completions and tool calling. After connecting either kind of provider, use `/model` to select the model.

## Reasoning settings for OpenAI-compatible gateways

An OpenAI-compatible gateway can expose models from multiple providers, including Claude models, through the Chat Completions API. The standard `/v1/models` response often contains only model IDs, so Letta cannot reliably infer the reasoning levels supported by every routed model.

For models connected through a BYOK OpenAI-compatible custom provider, the model selector includes a reasoning control. Letta sends an explicit selection in the OpenAI `reasoning_effort` field:

| Selection  | Value sent to the gateway               |
| ---------- | --------------------------------------- |
| Default    | The `reasoning_effort` field is omitted |
| Off        | `none`                                  |
| Minimal    | `minimal`                               |
| Low        | `low`                                   |
| Medium     | `medium`                                |
| High       | `high`                                  |
| Extra-High | `xhigh`                                 |
| Max        | `max`                                   |

The selector may show fewer levels when Letta recognizes the model’s supported options. For an unrecognized model behind a custom gateway, it exposes the full set so you can choose a level supported by your gateway. Use **Default** when the gateway or its model configuration should decide the reasoning level.

The gateway is responsible for accepting, remapping, or rejecting an explicit value. For example, [CLIProxyAPI](https://github.com/router-for-me/CLIProxyAPI) can serve Claude models through an OpenAI-compatible endpoint and translate `reasoning_effort` into Anthropic’s native reasoning controls. Other routers can apply their own equivalent mapping.

If a request fails only after choosing an explicit reasoning level, confirm that your gateway supports that value. Select **Default** to omit `reasoning_effort` and return control to the gateway.

| Provider                                                                                         | Local support          | Signed in with Letta   |
| ------------------------------------------------------------------------------------------------ | ---------------------- | ---------------------- |
| [Amazon Bedrock](https://platform.claude.com/docs/en/build-with-claude/claude-on-amazon-bedrock) | AWS credentials        | AWS credentials        |
| [Anthropic API](https://platform.claude.com/settings/keys)                                       | API key                | API key                |
| [Azure OpenAI Responses](https://azure.microsoft.com/en-us/products/ai-foundry/models/openai)    | API key                | —                      |
| [Cerebras](https://inference-docs.cerebras.ai)                                                   | API key                | —                      |
| [ChatGPT Plus/Pro Codex](https://developers.openai.com/codex/pricing/)                           | Subscription           | Subscription           |
| [Cloudflare AI Gateway](https://developers.cloudflare.com/ai-gateway/)                           | API key                | —                      |
| [Cloudflare Workers AI](https://developers.cloudflare.com/workers-ai/)                           | API key                | —                      |
| [DeepSeek](https://platform.deepseek.com/api_keys)                                               | API key                | —                      |
| [Fireworks](https://fireworks.ai/)                                                               | API key                | —                      |
| [GitHub Copilot](https://github.com/features/copilot)                                            | Subscription           | —                      |
| [Google Gemini](https://aistudio.google.com/app/api-keys)                                        | API key                | API key                |
| [Google Vertex AI](https://cloud.google.com/vertex-ai)                                           | API key                | —                      |
| [Groq](https://console.groq.com/keys)                                                            | API key                | —                      |
| [Hugging Face](https://huggingface.co/settings/tokens)                                           | API key                | —                      |
| [Kimi Code](https://platform.moonshot.ai/)                                                       | API key                | API key                |
| [llama.cpp](https://github.com/ggml-org/llama.cpp)                                               | Local endpoint         | —                      |
| [LM Studio](https://lmstudio.ai/)                                                                | Local endpoint         | —                      |
| [MiniMax](https://platform.minimax.io/docs/guides/quickstart-preparation)                        | API key or coding plan | API key or coding plan |
| [MiniMax (China)](https://platform.minimaxi.com/)                                                | API key                | —                      |
| [Mistral](https://console.mistral.ai/api-keys/)                                                  | API key                | —                      |
| [Moonshot AI](https://platform.moonshot.ai/)                                                     | API key                | API key                |
| [Moonshot AI (China)](https://platform.moonshot.cn/)                                             | API key                | —                      |
| [Ollama](https://ollama.com/)                                                                    | Local endpoint         | —                      |
| [Ollama Cloud](https://ollama.com/)                                                              | API key                | —                      |
| [OpenAI API](https://platform.openai.com/settings/organization/api-keys)                         | API key                | API key                |
| OpenAI-compatible API                                                                            | API key + base URL     | API key + base URL     |
| [OpenCode Go](https://opencode.ai/)                                                              | API key                | —                      |
| [OpenCode Zen](https://opencode.ai/)                                                             | API key                | —                      |
| [OpenRouter](https://openrouter.ai/docs/api-reference/authentication)                            | API key                | API key                |
| [Together AI](https://docs.together.ai/docs/quickstart)                                          | API key                | —                      |
| [Vercel AI Gateway](https://vercel.com/docs/ai-gateway)                                          | API key                | —                      |
| [xAI](https://console.x.ai/)                                                                     | API key                | —                      |
| [Xiaomi MiMo](https://github.com/XiaomiMiMo/MiMo)                                                | API key                | —                      |
| Xiaomi MiMo Token Plan (Amsterdam)                                                               | Token plan             | —                      |
| Xiaomi MiMo Token Plan (China)                                                                   | Token plan             | —                      |
| Xiaomi MiMo Token Plan (Singapore)                                                               | Token plan             | —                      |
| [zAI API](https://docs.z.ai/guides/overview/quick-start)                                         | API key                | API key                |
| [zAI Coding Plan](https://z.ai/subscribe)                                                        | Coding plan            | Coding plan            |
