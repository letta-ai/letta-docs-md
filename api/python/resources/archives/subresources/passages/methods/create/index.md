## Create Passage In Archive

`archives.passages.create(strarchive_id, PassageCreateParams**kwargs)  -> Passage`

**post** `/v1/archives/{archive_id}/passages`

Create a new passage in an archive.

This adds a passage to the archive and creates embeddings for vector storage.

### Parameters

- `archive_id: str`

  The ID of the archive in the format 'archive-<uuid4>'

- `text: str`

  The text content of the passage

- `created_at: Optional[str]`

  Optional creation datetime for the passage (ISO 8601 format)

- `metadata: Optional[Dict[str, object]]`

  Optional metadata for the passage

- `tags: Optional[Sequence[str]]`

  Optional tags for categorizing the passage

### Returns

- `class Passage: …`

  Representation of a passage, which is stored in archival memory.

  - `embedding: Optional[List[float]]`

    The embedding of the passage.

  - `embedding_config: Optional[EmbeddingConfig]`

    Configuration for embedding model connection and processing parameters.

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

  - `text: str`

    The text of the passage.

  - `id: Optional[str]`

    The human-friendly ID of the Passage

  - `archive_id: Optional[str]`

    The unique identifier of the archive containing this passage.

  - `created_at: Optional[datetime]`

    The creation date of the passage.

  - `created_by_id: Optional[str]`

    The id of the user that made this object.

  - `file_id: Optional[str]`

    The unique identifier of the file associated with the passage.

  - `file_name: Optional[str]`

    The name of the file (only for source passages).

  - `is_deleted: Optional[bool]`

    Whether this passage is deleted or not.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this object.

  - `metadata: Optional[Dict[str, object]]`

    The metadata of the passage.

  - `source_id: Optional[str]`

    Deprecated: Use `folder_id` field instead. The data source of the passage.

  - `tags: Optional[List[str]]`

    Tags associated with this passage.

  - `updated_at: Optional[datetime]`

    The timestamp when the object was last updated.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
passage = client.archives.passages.create(
    archive_id="archive-123e4567-e89b-42d3-8456-426614174000",
    text="text",
)
print(passage.id)
```

#### Response

```json
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
```
