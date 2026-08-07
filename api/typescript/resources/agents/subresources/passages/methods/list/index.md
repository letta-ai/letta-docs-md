## List Passages

`client.agents.passages.list(stringagentID, PassageListParamsquery?, RequestOptionsoptions?): PassageListResponse`

**get** `/v1/agents/{agent_id}/archival-memory`

Retrieve the memories in an agent's archival memory store (paginated query).

### Parameters

- `agentID: string`

  The ID of the agent in the format 'agent-<uuid4>'

- `query: PassageListParams`

  - `after?: string | null`

    Unique ID of the memory to start the query range at.

  - `ascending?: boolean | null`

    Whether to sort passages oldest to newest (True, default) or newest to oldest (False)

  - `before?: string | null`

    Unique ID of the memory to end the query range at.

  - `limit?: number | null`

    How many results to include in the response.

  - `search?: string | null`

    Search passages by text

### Returns

- `PassageListResponse = Array<Passage>`

  - `embedding: Array<number> | null`

    The embedding of the passage.

  - `embedding_config: EmbeddingConfig | null`

    Configuration for embedding model connection and processing parameters.

    - `embedding_dim: number`

      The dimension of the embedding.

    - `embedding_endpoint_type: "openai" | "anthropic" | "bedrock" | 16 more`

      The endpoint type for the model.

      - `"openai"`

      - `"anthropic"`

      - `"bedrock"`

      - `"google_ai"`

      - `"google_vertex"`

      - `"azure"`

      - `"groq"`

      - `"ollama"`

      - `"webui"`

      - `"webui-legacy"`

      - `"lmstudio"`

      - `"lmstudio-legacy"`

      - `"llamacpp"`

      - `"koboldcpp"`

      - `"vllm"`

      - `"hugging-face"`

      - `"mistral"`

      - `"together"`

      - `"pinecone"`

    - `embedding_model: string`

      The model for the embedding.

    - `azure_deployment?: string | null`

      The Azure deployment for the model.

    - `azure_endpoint?: string | null`

      The Azure endpoint for the model.

    - `azure_version?: string | null`

      The Azure version for the model.

    - `batch_size?: number`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size?: number | null`

      The chunk size of the embedding.

    - `embedding_endpoint?: string | null`

      The endpoint for the model (`None` if local).

    - `handle?: string | null`

      The handle for this config, in the format provider/model-name.

  - `text: string`

    The text of the passage.

  - `id?: string`

    The human-friendly ID of the Passage

  - `archive_id?: string | null`

    The unique identifier of the archive containing this passage.

  - `created_at?: string | null`

    The creation date of the passage.

  - `created_by_id?: string | null`

    The id of the user that made this object.

  - `file_id?: string | null`

    The unique identifier of the file associated with the passage.

  - `file_name?: string | null`

    The name of the file (only for source passages).

  - `is_deleted?: boolean`

    Whether this passage is deleted or not.

  - `last_updated_by_id?: string | null`

    The id of the user that made this object.

  - `metadata?: Record<string, unknown> | null`

    The metadata of the passage.

  - `source_id?: string | null`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags?: Array<string> | null`

    Tags associated with this passage.

  - `updated_at?: string | null`

    The timestamp when the object was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const passages = await client.agents.passages.list('agent-123e4567-e89b-42d3-8456-426614174000');

console.log(passages);
```

#### Response

```json
[
  {
    "embedding": [
      0
    ],
    "embedding_config": {
      "embedding_dim": 0,
      "embedding_endpoint_type": "openai",
      "embedding_model": "embedding_model",
      "azure_deployment": "azure_deployment",
      "azure_endpoint": "azure_endpoint",
      "azure_version": "azure_version",
      "batch_size": 0,
      "embedding_chunk_size": 0,
      "embedding_endpoint": "embedding_endpoint",
      "handle": "handle"
    },
    "text": "text",
    "id": "passage-123e4567-e89b-12d3-a456-426614174000",
    "archive_id": "archive_id",
    "created_at": "2019-12-27T18:11:19.117Z",
    "created_by_id": "created_by_id",
    "file_id": "file_id",
    "file_name": "file_name",
    "is_deleted": true,
    "last_updated_by_id": "last_updated_by_id",
    "metadata": {
      "foo": "bar"
    },
    "source_id": "source_id",
    "tags": [
      "string"
    ],
    "updated_at": "2019-12-27T18:11:19.117Z"
  }
]
```
