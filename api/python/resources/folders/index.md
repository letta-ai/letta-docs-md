# Folders

## Retrieve Folder

`folders.retrieve(strfolder_id)  -> Folder`

**get** `/v1/folders/{folder_id}`

Get a folder by ID

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

### Returns

- `class Folder: …`

  Representation of a folder, which is a collection of files and passages.

  - `id: str`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

    The name of the folder.

  - `created_at: Optional[datetime]`

    The timestamp when the folder was created.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `description: Optional[str]`

    The description of the folder.

  - `instructions: Optional[str]`

    Instructions for how to use the folder.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    Metadata associated with the folder.

  - `updated_at: Optional[datetime]`

    The timestamp when the folder was last updated.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
folder = client.folders.retrieve(
    "source-123e4567-e89b-42d3-8456-426614174000",
)
print(folder.id)
```

#### Response

```json
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
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```

## Update Folder

`folders.update(strfolder_id, FolderUpdateParams**kwargs)  -> Folder`

**patch** `/v1/folders/{folder_id}`

Update the name or documentation of an existing data folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `description: Optional[str]`

  The description of the source.

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

- `instructions: Optional[str]`

  Instructions for how to use the source.

- `metadata: Optional[Dict[str, object]]`

  Metadata associated with the source.

- `name: Optional[str]`

  The name of the source.

### Returns

- `class Folder: …`

  Representation of a folder, which is a collection of files and passages.

  - `id: str`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

    The name of the folder.

  - `created_at: Optional[datetime]`

    The timestamp when the folder was created.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `description: Optional[str]`

    The description of the folder.

  - `instructions: Optional[str]`

    Instructions for how to use the folder.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    Metadata associated with the folder.

  - `updated_at: Optional[datetime]`

    The timestamp when the folder was last updated.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
folder = client.folders.update(
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
print(folder.id)
```

#### Response

```json
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
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```

## Delete Folder

`folders.delete(strfolder_id)  -> object`

**delete** `/v1/folders/{folder_id}`

Delete a data folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
folder = client.folders.delete(
    "source-123e4567-e89b-42d3-8456-426614174000",
)
print(folder)
```

#### Response

```json
{}
```

## List Folders

`folders.list(FolderListParams**kwargs)  -> SyncArrayPage[Folder]`

**get** `/v1/folders/`

List all data folders created by a user.

### Parameters

- `after: Optional[str]`

  Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

- `limit: Optional[int]`

  Maximum number of folders to return

- `name: Optional[str]`

  Folder name to filter by

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for folders by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `class Folder: …`

  Representation of a folder, which is a collection of files and passages.

  - `id: str`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

    The name of the folder.

  - `created_at: Optional[datetime]`

    The timestamp when the folder was created.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `description: Optional[str]`

    The description of the folder.

  - `instructions: Optional[str]`

    Instructions for how to use the folder.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    Metadata associated with the folder.

  - `updated_at: Optional[datetime]`

    The timestamp when the folder was last updated.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.folders.list()
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
    "updated_at": "2019-12-27T18:11:19.117Z"
  }
]
```

## Create Folder

`folders.create(FolderCreateParams**kwargs)  -> Folder`

**post** `/v1/folders/`

Create a new data folder.

### Parameters

- `name: str`

  The name of the source.

- `description: Optional[str]`

  The description of the source.

- `embedding: Optional[str]`

  The handle for the embedding config used by the source.

- `embedding_chunk_size: Optional[int]`

  The chunk size of the embedding.

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

- `instructions: Optional[str]`

  Instructions for how to use the source.

- `metadata: Optional[Dict[str, object]]`

  Metadata associated with the source.

### Returns

- `class Folder: …`

  Representation of a folder, which is a collection of files and passages.

  - `id: str`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

    The name of the folder.

  - `created_at: Optional[datetime]`

    The timestamp when the folder was created.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `description: Optional[str]`

    The description of the folder.

  - `instructions: Optional[str]`

    Instructions for how to use the folder.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    Metadata associated with the folder.

  - `updated_at: Optional[datetime]`

    The timestamp when the folder was last updated.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
folder = client.folders.create(
    name="name",
)
print(folder.id)
```

#### Response

```json
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
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```

## Domain Types

### Folder

- `class Folder: …`

  Representation of a folder, which is a collection of files and passages.

  - `id: str`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

    The name of the folder.

  - `created_at: Optional[datetime]`

    The timestamp when the folder was created.

  - `created_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `description: Optional[str]`

    The description of the folder.

  - `instructions: Optional[str]`

    Instructions for how to use the folder.

  - `last_updated_by_id: Optional[str]`

    The id of the user that made this Tool.

  - `metadata: Optional[Dict[str, object]]`

    Metadata associated with the folder.

  - `updated_at: Optional[datetime]`

    The timestamp when the folder was last updated.

# Files

## Upload File To Folder

`folders.files.upload(strfolder_id, FileUploadParams**kwargs)  -> FileUploadResponse`

**post** `/v1/folders/{folder_id}/upload`

Upload a file to a data folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `file: FileTypes`

- `duplicate_handling: Optional[Literal["skip", "error", "suffix", "replace"]]`

  How to handle duplicate filenames

  - `"skip"`

  - `"error"`

  - `"suffix"`

  - `"replace"`

- `name: Optional[str]`

  Optional custom name to override the uploaded file's name

### Returns

- `class FileUploadResponse: …`

  Representation of a single FileMetadata

  - `id: str`

    The human-friendly ID of the File

  - `source_id: str`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded: Optional[int]`

    Number of chunks that have been embedded.

  - `content: Optional[str]`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at: Optional[datetime]`

    The creation date of the file.

  - `error_message: Optional[str]`

    Optional error message if the file failed processing.

  - `file_creation_date: Optional[str]`

    The creation date of the file.

  - `file_last_modified_date: Optional[str]`

    The last modified date of the file.

  - `file_name: Optional[str]`

    The name of the file.

  - `file_path: Optional[str]`

    The path to the file.

  - `file_size: Optional[int]`

    The size of the file in bytes.

  - `file_type: Optional[str]`

    The type of the file (MIME type).

  - `original_file_name: Optional[str]`

    The original name of the file as uploaded.

  - `processing_status: Optional[Literal["pending", "parsing", "embedding", 2 more]]`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks: Optional[int]`

    Total number of chunks for the file.

  - `updated_at: Optional[datetime]`

    The update date of the file.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
response = client.folders.files.upload(
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
    file=b"Example data",
)
print(response.id)
```

#### Response

```json
{
  "id": "file-123e4567-e89b-12d3-a456-426614174000",
  "source_id": "source_id",
  "chunks_embedded": 0,
  "content": "content",
  "created_at": "2019-12-27T18:11:19.117Z",
  "error_message": "error_message",
  "file_creation_date": "file_creation_date",
  "file_last_modified_date": "file_last_modified_date",
  "file_name": "file_name",
  "file_path": "file_path",
  "file_size": 0,
  "file_type": "file_type",
  "original_file_name": "original_file_name",
  "processing_status": "pending",
  "total_chunks": 0,
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```

## List Files For Folder

`folders.files.list(strfolder_id, FileListParams**kwargs)  -> SyncArrayPage[FileListResponse]`

**get** `/v1/folders/{folder_id}/files`

List paginated files associated with a data folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `after: Optional[str]`

  Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

- `include_content: Optional[bool]`

  Whether to include full file content

- `limit: Optional[int]`

  Maximum number of files to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for files by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `class FileListResponse: …`

  Representation of a single FileMetadata

  - `id: str`

    The human-friendly ID of the File

  - `source_id: str`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded: Optional[int]`

    Number of chunks that have been embedded.

  - `content: Optional[str]`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at: Optional[datetime]`

    The creation date of the file.

  - `error_message: Optional[str]`

    Optional error message if the file failed processing.

  - `file_creation_date: Optional[str]`

    The creation date of the file.

  - `file_last_modified_date: Optional[str]`

    The last modified date of the file.

  - `file_name: Optional[str]`

    The name of the file.

  - `file_path: Optional[str]`

    The path to the file.

  - `file_size: Optional[int]`

    The size of the file in bytes.

  - `file_type: Optional[str]`

    The type of the file (MIME type).

  - `original_file_name: Optional[str]`

    The original name of the file as uploaded.

  - `processing_status: Optional[Literal["pending", "parsing", "embedding", 2 more]]`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks: Optional[int]`

    Total number of chunks for the file.

  - `updated_at: Optional[datetime]`

    The update date of the file.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
page = client.folders.files.list(
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
page = page.items[0]
print(page.id)
```

#### Response

```json
[
  {
    "id": "file-123e4567-e89b-12d3-a456-426614174000",
    "source_id": "source_id",
    "chunks_embedded": 0,
    "content": "content",
    "created_at": "2019-12-27T18:11:19.117Z",
    "error_message": "error_message",
    "file_creation_date": "file_creation_date",
    "file_last_modified_date": "file_last_modified_date",
    "file_name": "file_name",
    "file_path": "file_path",
    "file_size": 0,
    "file_type": "file_type",
    "original_file_name": "original_file_name",
    "processing_status": "pending",
    "total_chunks": 0,
    "updated_at": "2019-12-27T18:11:19.117Z"
  }
]
```

## Retrieve File

`folders.files.retrieve(strfile_id, FileRetrieveParams**kwargs)  -> FileRetrieveResponse`

**get** `/v1/folders/{folder_id}/files/{file_id}`

Retrieve a file from a folder by ID.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `file_id: str`

  The ID of the file in the format 'file-<uuid4>'

- `include_content: Optional[bool]`

  Whether to include full file content

### Returns

- `class FileRetrieveResponse: …`

  Representation of a single FileMetadata

  - `id: str`

    The human-friendly ID of the File

  - `source_id: str`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded: Optional[int]`

    Number of chunks that have been embedded.

  - `content: Optional[str]`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at: Optional[datetime]`

    The creation date of the file.

  - `error_message: Optional[str]`

    Optional error message if the file failed processing.

  - `file_creation_date: Optional[str]`

    The creation date of the file.

  - `file_last_modified_date: Optional[str]`

    The last modified date of the file.

  - `file_name: Optional[str]`

    The name of the file.

  - `file_path: Optional[str]`

    The path to the file.

  - `file_size: Optional[int]`

    The size of the file in bytes.

  - `file_type: Optional[str]`

    The type of the file (MIME type).

  - `original_file_name: Optional[str]`

    The original name of the file as uploaded.

  - `processing_status: Optional[Literal["pending", "parsing", "embedding", 2 more]]`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks: Optional[int]`

    Total number of chunks for the file.

  - `updated_at: Optional[datetime]`

    The update date of the file.

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
file = client.folders.files.retrieve(
    file_id="file-123e4567-e89b-42d3-8456-426614174000",
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
print(file.id)
```

#### Response

```json
{
  "id": "file-123e4567-e89b-12d3-a456-426614174000",
  "source_id": "source_id",
  "chunks_embedded": 0,
  "content": "content",
  "created_at": "2019-12-27T18:11:19.117Z",
  "error_message": "error_message",
  "file_creation_date": "file_creation_date",
  "file_last_modified_date": "file_last_modified_date",
  "file_name": "file_name",
  "file_path": "file_path",
  "file_size": 0,
  "file_type": "file_type",
  "original_file_name": "original_file_name",
  "processing_status": "pending",
  "total_chunks": 0,
  "updated_at": "2019-12-27T18:11:19.117Z"
}
```

## Delete File From Folder

`folders.files.delete(strfile_id, FileDeleteParams**kwargs)`

**delete** `/v1/folders/{folder_id}/{file_id}`

Delete a file from a folder.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `file_id: str`

  The ID of the file in the format 'file-<uuid4>'

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
client.folders.files.delete(
    file_id="file-123e4567-e89b-42d3-8456-426614174000",
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
```

## Domain Types

### File Upload Response

- `class FileUploadResponse: …`

  Representation of a single FileMetadata

  - `id: str`

    The human-friendly ID of the File

  - `source_id: str`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded: Optional[int]`

    Number of chunks that have been embedded.

  - `content: Optional[str]`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at: Optional[datetime]`

    The creation date of the file.

  - `error_message: Optional[str]`

    Optional error message if the file failed processing.

  - `file_creation_date: Optional[str]`

    The creation date of the file.

  - `file_last_modified_date: Optional[str]`

    The last modified date of the file.

  - `file_name: Optional[str]`

    The name of the file.

  - `file_path: Optional[str]`

    The path to the file.

  - `file_size: Optional[int]`

    The size of the file in bytes.

  - `file_type: Optional[str]`

    The type of the file (MIME type).

  - `original_file_name: Optional[str]`

    The original name of the file as uploaded.

  - `processing_status: Optional[Literal["pending", "parsing", "embedding", 2 more]]`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks: Optional[int]`

    Total number of chunks for the file.

  - `updated_at: Optional[datetime]`

    The update date of the file.

### File List Response

- `class FileListResponse: …`

  Representation of a single FileMetadata

  - `id: str`

    The human-friendly ID of the File

  - `source_id: str`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded: Optional[int]`

    Number of chunks that have been embedded.

  - `content: Optional[str]`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at: Optional[datetime]`

    The creation date of the file.

  - `error_message: Optional[str]`

    Optional error message if the file failed processing.

  - `file_creation_date: Optional[str]`

    The creation date of the file.

  - `file_last_modified_date: Optional[str]`

    The last modified date of the file.

  - `file_name: Optional[str]`

    The name of the file.

  - `file_path: Optional[str]`

    The path to the file.

  - `file_size: Optional[int]`

    The size of the file in bytes.

  - `file_type: Optional[str]`

    The type of the file (MIME type).

  - `original_file_name: Optional[str]`

    The original name of the file as uploaded.

  - `processing_status: Optional[Literal["pending", "parsing", "embedding", 2 more]]`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks: Optional[int]`

    Total number of chunks for the file.

  - `updated_at: Optional[datetime]`

    The update date of the file.

### File Retrieve Response

- `class FileRetrieveResponse: …`

  Representation of a single FileMetadata

  - `id: str`

    The human-friendly ID of the File

  - `source_id: str`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded: Optional[int]`

    Number of chunks that have been embedded.

  - `content: Optional[str]`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at: Optional[datetime]`

    The creation date of the file.

  - `error_message: Optional[str]`

    Optional error message if the file failed processing.

  - `file_creation_date: Optional[str]`

    The creation date of the file.

  - `file_last_modified_date: Optional[str]`

    The last modified date of the file.

  - `file_name: Optional[str]`

    The name of the file.

  - `file_path: Optional[str]`

    The path to the file.

  - `file_size: Optional[int]`

    The size of the file in bytes.

  - `file_type: Optional[str]`

    The type of the file (MIME type).

  - `original_file_name: Optional[str]`

    The original name of the file as uploaded.

  - `processing_status: Optional[Literal["pending", "parsing", "embedding", 2 more]]`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks: Optional[int]`

    Total number of chunks for the file.

  - `updated_at: Optional[datetime]`

    The update date of the file.

# Agents

## List Agents For Folder

`folders.agents.list(strfolder_id, AgentListParams**kwargs)  -> AgentListResponse`

**get** `/v1/folders/{folder_id}/agents`

Get all agent IDs that have the specified folder attached.

### Parameters

- `folder_id: str`

  The ID of the source in the format 'source-<uuid4>'

- `after: Optional[str]`

  Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

- `before: Optional[str]`

  Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

- `limit: Optional[int]`

  Maximum number of agents to return

- `order: Optional[Literal["asc", "desc"]]`

  Sort order for agents by creation time. 'asc' for oldest first, 'desc' for newest first

  - `"asc"`

  - `"desc"`

- `order_by: Optional[Literal["created_at"]]`

  Field to sort by

  - `"created_at"`

### Returns

- `List[str]`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
agents = client.folders.agents.list(
    folder_id="source-123e4567-e89b-42d3-8456-426614174000",
)
print(agents)
```

#### Response

```json
[
  "string"
]
```

## Domain Types

### Agent List Response

- `List[str]`
