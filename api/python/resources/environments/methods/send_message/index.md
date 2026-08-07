## Send Message to Environment

`environments.send_message(strconnection_id, EnvironmentSendMessageParams**kwargs)  -> EnvironmentSendMessageResponse`

**post** `/v1/environments/{connectionId}/messages`

Send a message to a specific environment connection

### Parameters

- `connection_id: str`

- `messages: Iterable[Message]`

  - `class MessageUnionMember0: …`

    - `client_message_id: str`

    - `content: Union[str, Iterable[MessageUnionMember0ContentUnionMember1]]`

      - `str`

      - `Iterable[MessageUnionMember0ContentUnionMember1]`

        - `text: str`

        - `type: Literal["text"]`

          - `"text"`

    - `role: Literal["user"]`

      - `"user"`

    - `otid: Optional[str]`

  - `class MessageUnionMember1: …`

    - `approvals: Iterable[MessageUnionMember1Approval]`

      - `class MessageUnionMember1ApprovalUnionMember0: …`

        - `status: Literal["success", "error"]`

          - `"success"`

          - `"error"`

        - `tool_call_id: str`

        - `tool_return: Union[str, Iterable[MessageUnionMember1ApprovalUnionMember0ToolReturnUnionMember1]]`

          - `str`

          - `Iterable[MessageUnionMember1ApprovalUnionMember0ToolReturnUnionMember1]`

            - `text: str`

            - `type: Literal["text"]`

              - `"text"`

        - `stderr: Optional[Sequence[str]]`

        - `stdout: Optional[Sequence[str]]`

        - `type: Optional[Literal["tool"]]`

          - `"tool"`

      - `class MessageUnionMember1ApprovalUnionMember1: …`

        - `approve: bool`

        - `tool_call_id: str`

        - `reason: Optional[str]`

        - `type: Optional[Literal["approval"]]`

          - `"approval"`

        - `updated_input: Optional[Dict[str, object]]`

    - `type: Literal["approval"]`

      - `"approval"`

- `agent_id: Optional[str]`

- `conversation_id: Optional[str]`

### Returns

- `class EnvironmentSendMessageResponse: …`

  - `message: str`

  - `success: bool`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.environments.send_message(
    connection_id="connectionId",
    messages=[{
        "client_message_id": "client_message_id",
        "content": "string",
        "role": "user",
    }],
)
print(response.message)
```

#### Response

```json
{
  "message": "message",
  "success": true
}
```
