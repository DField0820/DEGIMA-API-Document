# Create chat completion

```http
POST https://cyber.degima.ai:11000/v1/chat/completions
```

## Request body

| Field      | Type  | Required | Description |
|------------|-------|----------|-------------|
| `messages` | array | **Yes** | A list of messages that make up the conversation so far. |
| `model` | string | **Yes** | The ID of the model used to generate the response, e.g., `degima/gemma2`. |
| `frequency_penalty` | number or null | Optional | A value between -2.0 and 2.0. Positive values penalize tokens based on their frequency in the text so far, reducing the chance of repetition. Default is 0. |
| `max_tokens` | integer or null | Optional | The maximum number of tokens that can be generated. |
| `presence_penalty` | number or null | Optional | A value between -2.0 and 2.0. Positive values penalize tokens based on whether they have appeared before, encouraging new topics. Default is 0. |
| `response_format` | object | Optional | Specifies the output format. For structured output, use: `{ "type": "json_schema", "json_schema": {...} }`. |
| `stop` | string or null | Optional | A single sequence at which the API will stop generating further tokens. The stop sequence itself is not included in the output. Default is null. |
| `temperature` | number or null | Optional | Sampling temperature (0 to 2). Higher values (e.g., 0.8) make outputs more random, lower values (e.g., 0.2) make them more focused. Recommended to adjust either this or top_p, not both. Default is 1. |
| `top_p` | number or null | Optional | Nucleus sampling parameter. When set to 0.1, only tokens comprising the top 10% of probability mass are considered. Recommended to adjust either this or temperature, not both. Default is 1. |

## Returns

| Field      | Type  | Description |
|------------|-------|-------------|
| `choices` | array | A list of chat completion results. Each includes `finish_reason`, `index`, `logprobs`, and `message` (which contains `content` and `role`). |
| `usage` | object | Usage statistics for the completion request. Includes `completion_tokens` (number of tokens in the output), `prompt_tokens` (tokens in the input), and `total_tokens` (sum of both). |
| `timings` | object | Processing time statistics. `prompt_n`: number of uncached prompt tokens; `prompt_ms`: time to process them; `prompt_per_second`: tokens processed per second; `prompt_per_token_ms`: inverse. `predicted_n`: number of generated tokens (same as `completion_tokens`); `predicted_ms`: time to generate them; `predicted_per_second` and `predicted_per_token_ms`: related speed metrics. |


### The chat completion object:
```
{
  "id": "chatcmpl-3WGXkV6LFVBcTgUM2Mk6S1VWCdEd9m5K",
  "choices": [
    {
      "finish_reason": "stop",
      "index": 0,
      "logprobs": null,
      "message": {
        "content": "Y \n",
        "role": "assistant",
        "function_call": null,
        "tool_calls": null
      }
    }
  ],
  "created": 1745310378,
  "model": "degima/gemma2",
  "object": "chat.completion",
  "service_tier": null,
  "system_fingerprint": "b4741-9626d935",
  "usage": {
    "completion_tokens": 4,
    "prompt_tokens": 2143,
    "total_tokens": 2147
  },
  "timings": {
    "prompt_n": 17,
    "prompt_ms": 98.626,
    "prompt_per_token_ms": 5.801529411764706,
    "prompt_per_second": 172.36834100541438,
    "predicted_n": 4,
    "predicted_ms": 57.514,
    "predicted_per_token_ms": 14.3785,
    "predicted_per_second": 69.54828389609486
  }
}
```
