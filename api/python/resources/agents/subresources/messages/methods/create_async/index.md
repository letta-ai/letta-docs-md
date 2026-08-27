## Create Message Async

`agents.messages.create_async(stragent_id, MessageCreateAsyncParams**kwargs)  -> Run`

**post** `/v1/agents/{agent_id}/messages/async`

Asynchronously process a user message and return a run object.
The actual processing happens in the background, and the status can be checked using the run ID.

This is "asynchronous" in the sense that it's a background run and explicitly must be fetched by the run ID.

**Note:** Sending multiple concurrent requests to the same agent can lead to undefined behavior.
Each agent processes messages sequentially, and concurrent requests may interleave in unexpected ways.
Wait for each request to complete before sending the next one. Use separate agents or conversations for parallel processing.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `assistant_message_tool_kwarg: Optional[str]`

  The name of the message argument in the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

- `assistant_message_tool_name: Optional[str]`

  The name of the designated message tool. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

- `callback_url: Optional[str]`

  Optional callback URL to POST to when the job completes

- `client_skills: Optional[Iterable[ClientSkill]]`

  Client-side skills available in the environment. These are rendered in the system prompt's available skills section alongside agent-scoped skills from MemFS.

  - `description: str`

    Description of what the skill does

  - `location: str`

    Path or location hint for the skill (e.g. skills/my-skill/SKILL.md)

  - `name: str`

    The name of the skill

- `client_tools: Optional[Iterable[ClientTool]]`

  Client-side tools that the agent can call. When the agent calls a client-side tool, execution pauses and returns control to the client to execute the tool and provide the result via a ToolReturn.

  - `name: str`

    The name of the tool function

  - `description: Optional[str]`

    Description of what the tool does

  - `parameters: Optional[Dict[str, object]]`

    JSON Schema for the function parameters

- `enable_thinking: Optional[str]`

  If set to True, enables reasoning before responses or tool calls from the agent.

- `include_compaction_messages: Optional[bool]`

  If True, compaction events emit structured `SummaryMessage` and `EventMessage` types. If False (default), compaction messages are not included in the response.

- `include_return_message_types: Optional[List[MessageType]]`

  Only return specified message types in the response. If `None` (default) returns all messages.

  - `"system_message"`

  - `"user_message"`

  - `"assistant_message"`

  - `"reasoning_message"`

  - `"hidden_reasoning_message"`

  - `"tool_call_message"`

  - `"tool_return_message"`

  - `"approval_request_message"`

  - `"approval_response_message"`

  - `"summary_message"`

  - `"event_message"`

- `input: Optional[Union[str, Iterable[InputUnionMember1], null]]`

  Syntactic sugar for a single user message. Equivalent to messages=[{'role': 'user', 'content': input}].

  - `str`

  - `Iterable[InputUnionMember1]`

    - `class TextContent: …`

      - `text: str`

        The text content of the message.

      - `signature: Optional[str]`

        Stores a unique identifier for any reasoning associated with this text content.

      - `type: Optional[Literal["text"]]`

        The type of the message.

        - `"text"`

    - `class ImageContent: …`

      - `source: Source`

        The source of the image.

        - `class SourceURLImage: …`

          - `url: str`

            The URL of the image.

          - `type: Optional[Literal["url"]]`

            The source type for the image.

            - `"url"`

        - `class SourceBase64Image: …`

          - `data: str`

            The base64 encoded image data.

          - `media_type: str`

            The media type for the image.

          - `detail: Optional[str]`

            What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

          - `type: Optional[Literal["base64"]]`

            The source type for the image.

            - `"base64"`

        - `class SourceLettaImage: …`

          - `file_id: str`

            The unique identifier of the image file persisted in storage.

          - `data: Optional[str]`

            The base64 encoded image data.

          - `detail: Optional[str]`

            What level of detail to use when processing and understanding the image (low, high, or auto to let the model decide)

          - `media_type: Optional[str]`

            The media type for the image.

          - `type: Optional[Literal["letta"]]`

            The source type for the image.

            - `"letta"`

      - `type: Optional[Literal["image"]]`

        The type of the message.

        - `"image"`

    - `class ToolCallContent: …`

      - `id: str`

        A unique identifier for this specific tool call instance.

      - `input: Dict[str, object]`

        The parameters being passed to the tool, structured as a dictionary of parameter names to values.

      - `name: str`

        The name of the tool being called.

      - `signature: Optional[str]`

        Stores a unique identifier for any reasoning associated with this tool call.

      - `type: Optional[Literal["tool_call"]]`

        Indicates this content represents a tool call event.

        - `"tool_call"`

    - `class ToolReturnContent: …`

      - `content: str`

        The content returned by the tool execution.

      - `is_error: bool`

        Indicates whether the tool execution resulted in an error.

      - `tool_call_id: str`

        References the ID of the ToolCallContent that initiated this tool call.

      - `type: Optional[Literal["tool_return"]]`

        Indicates this content represents a tool return event.

        - `"tool_return"`

    - `class ReasoningContent: …`

      Sent via the Anthropic Messages API

      - `is_native: bool`

        Whether the reasoning content was generated by a reasoner model that processed this step.

      - `reasoning: str`

        The intermediate reasoning or thought process content.

      - `signature: Optional[str]`

        A unique identifier for this reasoning step.

      - `type: Optional[Literal["reasoning"]]`

        Indicates this is a reasoning/intermediate step.

        - `"reasoning"`

    - `class RedactedReasoningContent: …`

      Sent via the Anthropic Messages API

      - `data: str`

        The redacted or filtered intermediate reasoning content.

      - `type: Optional[Literal["redacted_reasoning"]]`

        Indicates this is a redacted thinking step.

        - `"redacted_reasoning"`

    - `class OmittedReasoningContent: …`

      A placeholder for reasoning content we know is present, but isn't returned by the provider (e.g. OpenAI GPT-5 on ChatCompletions)

      - `signature: Optional[str]`

        A unique identifier for this reasoning step.

      - `type: Optional[Literal["omitted_reasoning"]]`

        Indicates this is an omitted reasoning step.

        - `"omitted_reasoning"`

    - `class InputUnionMember1SummarizedReasoningContent: …`

      The style of reasoning content returned by the OpenAI Responses API

      - `id: str`

        The unique identifier for this reasoning step.

      - `summary: Iterable[InputUnionMember1SummarizedReasoningContentSummary]`

        Summaries of the reasoning content.

        - `index: int`

          The index of the summary part.

        - `text: str`

          The text of the summary part.

      - `encrypted_content: Optional[str]`

        The encrypted reasoning content.

      - `type: Optional[Literal["summarized_reasoning"]]`

        Indicates this is a summarized reasoning step.

        - `"summarized_reasoning"`

- `max_steps: Optional[int]`

  Maximum number of steps the agent should take to process the request.

- `messages: Optional[Iterable[Message]]`

  The messages to be sent to the agent.

  - `class MessageCreate: …`

    Request to create a message

    - `content: Union[List[LettaMessageContentUnion], str]`

      The content of the message.

      - `List[LettaMessageContentUnion]`

        - `class TextContent: …`

        - `class ImageContent: …`

        - `class ToolCallContent: …`

        - `class ToolReturnContent: …`

        - `class ReasoningContent: …`

          Sent via the Anthropic Messages API

        - `class RedactedReasoningContent: …`

          Sent via the Anthropic Messages API

        - `class OmittedReasoningContent: …`

          A placeholder for reasoning content we know is present, but isn't returned by the provider (e.g. OpenAI GPT-5 on ChatCompletions)

      - `str`

    - `role: Literal["user", "system", "assistant"]`

      The role of the participant.

      - `"user"`

      - `"system"`

      - `"assistant"`

    - `batch_item_id: Optional[str]`

      The id of the LLMBatchItem that this message is associated with

    - `group_id: Optional[str]`

      The multi-agent group that the message was sent in

    - `name: Optional[str]`

      The name of the participant.

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `sender_id: Optional[str]`

      The id of the sender of the message, can be an identity id or agent id

    - `type: Optional[Literal["message"]]`

      The message type to be created.

      - `"message"`

  - `class ApprovalCreate: …`

    Input to approve or deny a tool call request

    - `approval_request_id: Optional[str]`

      The message ID of the approval request

    - `approvals: Optional[List[Approval]]`

      The list of approval responses

      - `class ApprovalReturn: …`

        - `approve: bool`

          Whether the tool has been approved

        - `tool_call_id: str`

          The ID of the tool call that corresponds to this approval

        - `reason: Optional[str]`

          An optional explanation for the provided approval status

        - `type: Optional[Literal["approval"]]`

          The message type to be created.

          - `"approval"`

      - `class ToolReturn: …`

        - `status: Literal["success", "error"]`

          - `"success"`

          - `"error"`

        - `tool_call_id: str`

        - `tool_return: Union[List[ToolReturnUnionMember0], str]`

          The tool return value - either a string or list of content parts (text/image)

          - `List[ToolReturnUnionMember0]`

            - `class TextContent: …`

            - `class ImageContent: …`

          - `str`

        - `stderr: Optional[List[str]]`

        - `stdout: Optional[List[str]]`

        - `type: Optional[Literal["tool"]]`

          The message type to be created.

          - `"tool"`

    - `approve: Optional[bool]`

      Whether the tool has been approved

    - `group_id: Optional[str]`

      The multi-agent group that the message was sent in

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `reason: Optional[str]`

      An optional explanation for the provided approval status

    - `type: Optional[Literal["approval"]]`

      The message type to be created.

      - `"approval"`

  - `class MessageToolReturnCreate: …`

    Submit tool return(s) from client-side tool execution.

    This is the preferred way to send tool results back to the agent after
    client-side tool execution. It is equivalent to sending an ApprovalCreate
    with tool return approvals, but provides a cleaner API for the common case.

    - `tool_returns: Iterable[ToolReturnParam]`

      List of tool returns from client-side execution

      - `status: Literal["success", "error"]`

      - `tool_call_id: str`

      - `tool_return: Union[List[ToolReturnUnionMember0], str]`

        The tool return value - either a string or list of content parts (text/image)

      - `stderr: Optional[List[str]]`

      - `stdout: Optional[List[str]]`

      - `type: Optional[Literal["tool"]]`

        The message type to be created.

    - `group_id: Optional[str]`

      The multi-agent group that the message was sent in

    - `otid: Optional[str]`

      The offline threading id (OTID). Set by the client to deduplicate requests. Used for idempotency in background streaming mode — each message in a request must have a unique OTID. Retries of the same request should reuse the same OTIDs.

    - `type: Optional[Literal["tool_return"]]`

      The message type to be created.

      - `"tool_return"`

- `override_model: Optional[str]`

  Model handle to use for this request instead of the agent's default model. This allows sending a message to a different model without changing the agent's configuration.

- `override_system: Optional[str]`

  Optional per-request system prompt override. When set, this is passed directly to the underlying LLM request and bypasses the persisted/compiled system message for that request.

- `return_logprobs: Optional[bool]`

  If True, returns log probabilities of the output tokens in the response. Useful for RL training. Only supported for OpenAI-compatible providers (including SGLang).

- `return_token_ids: Optional[bool]`

  If True, returns token IDs and logprobs for ALL LLM generations in the agent step, not just the last one. Uses SGLang native /generate endpoint. Returns 'turns' field with TurnTokenData for each assistant/tool turn. Required for proper multi-turn RL training with loss masking.

- `top_logprobs: Optional[int]`

  Number of most likely tokens to return at each position (0-20). Requires return_logprobs=True.

- `use_assistant_message: Optional[bool]`

  Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects. Still supported for legacy agent types, but deprecated for letta_v1_agent onward.

### Returns

- `class Run: …`

  Representation of a run - a conversation or processing session for an agent. Runs track when agents process messages and maintain the relationship between agents, steps, and messages.

  - `id: str`

    The human-friendly ID of the Run

  - `agent_id: str`

    The unique identifier of the agent associated with the run.

  - `background: Optional[bool]`

    Whether the run was created in background mode.

  - `base_template_id: Optional[str]`

    The base template ID that the run belongs to.

  - `callback_error: Optional[str]`

    Optional error message from attempting to POST the callback endpoint.

  - `callback_sent_at: Optional[datetime]`

    Timestamp when the callback was last attempted.

  - `callback_status_code: Optional[int]`

    HTTP status code returned by the callback endpoint.

  - `callback_url: Optional[str]`

    If set, POST to this URL when the run completes.

  - `completed_at: Optional[datetime]`

    The timestamp when the run was completed.

  - `conversation_id: Optional[str]`

    The unique identifier of the conversation associated with the run.

  - `created_at: Optional[datetime]`

    The timestamp when the run was created.

  - `metadata: Optional[Dict[str, object]]`

    Additional metadata for the run.

  - `request_config: Optional[RequestConfig]`

    The request configuration for the run.

    - `assistant_message_tool_kwarg: Optional[str]`

      The name of the message argument in the designated message tool.

    - `assistant_message_tool_name: Optional[str]`

      The name of the designated message tool.

    - `include_return_message_types: Optional[List[MessageType]]`

      Only return specified message types in the response. If `None` (default) returns all messages.

      - `"system_message"`

      - `"user_message"`

      - `"assistant_message"`

      - `"reasoning_message"`

      - `"hidden_reasoning_message"`

      - `"tool_call_message"`

      - `"tool_return_message"`

      - `"approval_request_message"`

      - `"approval_response_message"`

      - `"summary_message"`

      - `"event_message"`

    - `use_assistant_message: Optional[bool]`

      Whether the server should parse specific tool call arguments (default `send_message`) as `AssistantMessage` objects.

  - `status: Optional[Literal["created", "running", "completed", 2 more]]`

    The current status of the run.

    - `"created"`

    - `"running"`

    - `"completed"`

    - `"failed"`

    - `"cancelled"`

  - `stop_reason: Optional[StopReasonType]`

    The reason why the run was stopped.

    - `"end_turn"`

    - `"error"`

    - `"llm_api_error"`

    - `"invalid_llm_response"`

    - `"invalid_tool_call"`

    - `"max_steps"`

    - `"max_tokens_exceeded"`

    - `"no_tool_call"`

    - `"tool_rule"`

    - `"cancelled"`

    - `"insufficient_credits"`

    - `"requires_approval"`

    - `"context_window_overflow_in_system_prompt"`

  - `total_duration_ns: Optional[int]`

    Total run duration in nanoseconds

  - `ttft_ns: Optional[int]`

    Time to first token for a run in nanoseconds

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
run = client.agents.messages.create_async(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
print(run.id)
```

#### Response

```json
{
  "id": "run-123e4567-e89b-12d3-a456-426614174000",
  "agent_id": "agent_id",
  "background": true,
  "base_template_id": "base_template_id",
  "callback_error": "callback_error",
  "callback_sent_at": "2019-12-27T18:11:19.117Z",
  "callback_status_code": 0,
  "callback_url": "callback_url",
  "completed_at": "2019-12-27T18:11:19.117Z",
  "conversation_id": "conversation_id",
  "created_at": "2019-12-27T18:11:19.117Z",
  "metadata": {
    "foo": "bar"
  },
  "request_config": {
    "assistant_message_tool_kwarg": "assistant_message_tool_kwarg",
    "assistant_message_tool_name": "assistant_message_tool_name",
    "include_return_message_types": [
      "system_message"
    ],
    "use_assistant_message": true
  },
  "status": "created",
  "stop_reason": "end_turn",
  "total_duration_ns": 0,
  "ttft_ns": 0
}
```
