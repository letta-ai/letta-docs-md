## List Folders For Agent

`agents.folders.list(stragent_id, FolderListParams**kwargs)  -> SyncArrayPage[FolderListResponse]`

**get** `/v1/agents/{agent_id}/folders`

Get the folders associated with an agent.

### Parameters

- `agent_id: str`

  The ID of the agent in the format 'agent-<uuid4>'

- `after: Optional[str]`

  Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

- `limit: Optional[int]`

  Maximum number of sources to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for sources by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `class FolderListResponse: …`

  (Deprecated: Use Folder) Representation of a source, which is a collection of files and passages.

  - `id: str`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the source.

    - `embedding_dim: int`

      The dimension of the embedding.

    - `embedding_endpoint_type: Literal["openai", "anthropic", "bedrock", 16 more]`

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

    - `embedding_model: str`

      The model for the embedding.

    - `azure_deployment: Optional[str]`

      The Azure deployment for the model.

    - `azure_endpoint: Optional[str]`

      The Azure endpoint for the model.

    - `azure_version: Optional[str]`

      The Azure version for the model.

    - `batch_size: Optional[int]`

      The maximum batch size for processing embeddings.

    - `embedding_chunk_size: Optional[int]`

      The chunk size of the embedding.

    - `embedding_endpoint: Optional[str]`

      The endpoint for the model (`None` if local).

    - `handle: Optional[str]`

      The handle for this config, in the format provider/model-name.

  - `name: str`

    The name of the source.

  - `created_at: Optional[datetime]`

    The timestamp when the source was created.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `description: Optional[str]`

    The description of the source.

  - `instructions: Optional[str]`

    Instructions for how to use the source.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    Metadata associated with the source.

  - `updated_at: Optional[datetime]`

    The timestamp when the source was last updated.

  - `vector_db_provider: Optional[VectorDBProvider]`

    The vector database provider used for this source's passages

    - `"native"`

    - `"tpuf"`

    - `"pinecone"`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.agents.folders.list(
    agent_id="agent-123e4567-e89b-42d3-8456-426614174000",
)
page = page.items[0]
print(page.id)
```

#### Response

```json
[
  {
    "id": "source-123e4567-e89b-12d3-a456-426614174000",
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
    "name": "name",
    "created_at": "2019-12-27T18:11:19.117Z",
    "created_by_id": "created_by_id",
    "description": "description",
    "instructions": "instructions",
    "last_updated_by_id": "last_updated_by_id",
    "metadata": {
      "foo": "bar"
    },
    "updated_at": "2019-12-27T18:11:19.117Z",
    "vector_db_provider": "native"
  }
]
```
