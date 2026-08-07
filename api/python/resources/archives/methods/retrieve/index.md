## Retrieve Archive

`archives.retrieve(strarchive_id)  -> Archive`

**get** `/v1/archives/{archive_id}`

Get a single archive by its ID.

### Parameters

- `archive_id: str`

  The ID of the archive in the format 'archive-<uuid4>'

### Returns

- `class Archive: …`

  Representation of an archive - a collection of archival passages that can be shared between agents.

  - `id: str`

    The human-friendly ID of the Archive

  - `created_at: datetime`

    The creation date of the archive

  - `name: str`

    The name of the archive

  - `created_by_id: Optional[str]`

    The id of the user that made this object.

  - `description: Optional[str]`

    A description of the archive

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

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this object.

  - `metadata: Optional[Dict[str, object]]`

    Additional metadata

  - `updated_at: Optional[datetime]`

    The timestamp when the object was last updated.

  - `vector_db_provider: Optional[VectorDBProvider]`

    The vector database provider used for this archive's passages

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
archive = client.archives.retrieve(
    "archive-123e4567-e89b-42d3-8456-426614174000",
)
print(archive.id)
```

#### Response

```json
{
  "id": "archive-123e4567-e89b-12d3-a456-426614174000",
  "created_at": "2019-12-27T18:11:19.117Z",
  "name": "name",
  "created_by_id": "created_by_id",
  "description": "description",
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
  "last_updated_by_id": "last_updated_by_id",
  "metadata": {
    "foo": "bar"
  },
  "updated_at": "2019-12-27T18:11:19.117Z",
  "vector_db_provider": "native"
}
```
