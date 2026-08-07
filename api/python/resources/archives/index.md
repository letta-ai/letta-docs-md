# Archives

## Create Archive

`archives.create(ArchiveCreateParams**kwargs)  -> Archive`

**post** `/v1/archives/`

Create a new archive.

### Parameters

- `name: str`

- `description: Optional[str]`

- `embedding: Optional[str]`

  Embedding model handle for the archive

- `embedding_config: Optional[EmbeddingConfigParam]`

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
archive = client.archives.create(
    name="name",
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

## List Archives

`archives.list(ArchiveListParams**kwargs)  -> SyncArrayPage[Archive]`

**get** `/v1/archives/`

Get a list of all archives for the current organization with optional filters and pagination.

### Parameters

- `after: Optional[str]`

  Cursor for pagination (archive ID). Returns results relative to this ID in the specified sort order. Expected format: 'archive-<uuid4>'

- `agent_id: Optional[str]`

  Only archives attached to this agent ID

- `before: Optional[str]`

  Cursor for pagination (archive ID). Returns results relative to this ID in the specified sort order. Expected format: 'archive-<uuid4>'

- `limit: Optional[int]`

  Maximum number of archives to return

- `name: Optional[str]`

  Filter by archive name (exact match)

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for archives by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

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
page = client.archives.list()
page = page.items[0]
print(page.id)
```

#### Response

```json
[
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
]
```

## Update Archive

`archives.update(strarchive_id, ArchiveUpdateParams**kwargs)  -> Archive`

**patch** `/v1/archives/{archive_id}`

Update an existing archive's name and/or description.

### Parameters

- `archive_id: str`

  The ID of the archive in the format 'archive-<uuid4>'

- `description: Optional[str]`

- `name: Optional[str]`

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
archive = client.archives.update(
    archive_id="archive-123e4567-e89b-42d3-8456-426614174000",
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

## Delete Archive

`archives.delete(strarchive_id)`

**delete** `/v1/archives/{archive_id}`

Delete an archive by its ID.

### Parameters

- `archive_id: str`

  The ID of the archive in the format 'archive-<uuid4>'

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
client.archives.delete(
    "archive-123e4567-e89b-42d3-8456-426614174000",
)
```

## Domain Types

### Archive

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

### Vector DB Provider

- `Literal["native", "tpuf", "pinecone"]`

  Supported vector database providers for archival memory

  - `"native"`

  - `"tpuf"`

  - `"pinecone"`

# Passages

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

## Create Passages In Archive

`archives.passages.create_many(strarchive_id, PassageCreateManyParams**kwargs)  -> PassageCreateManyResponse`

**post** `/v1/archives/{archive_id}/passages/batch`

Create multiple passages in an archive.

This adds passages to the archive and creates embeddings for vector storage.

### Parameters

- `archive_id: str`

  The ID of the archive in the format 'archive-<uuid4>'

- `passages: Iterable[Passage]`

  Passages to create in the archive

  - `text: str`

    The text content of the passage

  - `created_at: Optional[str]`

    Optional creation datetime for the passage (ISO 8601 format)

  - `metadata: Optional[Dict[str, object]]`

    Optional metadata for the passage

  - `tags: Optional[Sequence[str]]`

    Optional tags for categorizing the passage

### Returns

- `List[Passage]`

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
passages = client.archives.passages.create_many(
    archive_id="archive-123e4567-e89b-42d3-8456-426614174000",
    passages=[{
        "text": "text"
    }],
)
print(passages)
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

## Delete Passage From Archive

`archives.passages.delete(strpassage_id, PassageDeleteParams**kwargs)`

**delete** `/v1/archives/{archive_id}/passages/{passage_id}`

Delete a passage from an archive.

This permanently removes the passage from both the database and vector storage (if applicable).

### Parameters

- `archive_id: str`

  The ID of the archive in the format 'archive-<uuid4>'

- `passage_id: str`

  The ID of the passage in the format 'passage-<uuid4>'

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
client.archives.passages.delete(
    passage_id="passage-123e4567-e89b-42d3-8456-426614174000",
    archive_id="archive-123e4567-e89b-42d3-8456-426614174000",
)
```

## Domain Types

### Passage Create Many Response

- `List[Passage]`

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
