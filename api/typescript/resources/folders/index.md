# Folders

## Retrieve Folder

`client.folders.retrieve(stringfolderID, RequestOptionsoptions?): Folder`

**get** `/v1/folders/{folder_id}`

Get a folder by ID

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

### Returns

- `Folder`

  Representation of a folder, which is a collection of files and passages.

  - `id: string`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

  - `name: string`

    The name of the folder.

  - `created_at?: string | null`

    The timestamp when the folder was created.

  - `created_by_id?: string | null`

    The id of the user that made this Tool.

  - `description?: string | null`

    The description of the folder.

  - `instructions?: string | null`

    Instructions for how to use the folder.

  - `last_updated_by_id?: string | null`

    The id of the user that made this Tool.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the folder.

  - `updated_at?: string | null`

    The timestamp when the folder was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const folder = await client.folders.retrieve('source-123e4567-e89b-42d3-8456-426614174000');

console.log(folder.id);
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

`client.folders.update(stringfolderID, FolderUpdateParamsbody, RequestOptionsoptions?): Folder`

**patch** `/v1/folders/{folder_id}`

Update the name or documentation of an existing data folder.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

- `body: FolderUpdateParams`

  - `description?: string | null`

    The description of the source.

  - `embedding_config?: EmbeddingConfig | null`

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

  - `instructions?: string | null`

    Instructions for how to use the source.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the source.

  - `name?: string | null`

    The name of the source.

### Returns

- `Folder`

  Representation of a folder, which is a collection of files and passages.

  - `id: string`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

  - `name: string`

    The name of the folder.

  - `created_at?: string | null`

    The timestamp when the folder was created.

  - `created_by_id?: string | null`

    The id of the user that made this Tool.

  - `description?: string | null`

    The description of the folder.

  - `instructions?: string | null`

    Instructions for how to use the folder.

  - `last_updated_by_id?: string | null`

    The id of the user that made this Tool.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the folder.

  - `updated_at?: string | null`

    The timestamp when the folder was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const folder = await client.folders.update('source-123e4567-e89b-42d3-8456-426614174000');

console.log(folder.id);
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

`client.folders.delete(stringfolderID, RequestOptionsoptions?): FolderDeleteResponse`

**delete** `/v1/folders/{folder_id}`

Delete a data folder.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

### Returns

- `FolderDeleteResponse = unknown`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const folder = await client.folders.delete('source-123e4567-e89b-42d3-8456-426614174000');

console.log(folder);
```

#### Response

```json
{}
```

## List Folders

`client.folders.list(FolderListParamsquery?, RequestOptionsoptions?): ArrayPage<Folder>`

**get** `/v1/folders/`

List all data folders created by a user.

### Parameters

- `query: FolderListParams`

  - `after?: string | null`

    Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (source ID). Returns results relative to this ID in the specified sort order. Expected format: 'source-<uuid4>'

  - `limit?: number | null`

    Maximum number of folders to return

  - `name?: string | null`

    Folder name to filter by

  - `order?: "asc" | "desc"`

    Sort order for folders by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `Folder`

  Representation of a folder, which is a collection of files and passages.

  - `id: string`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

  - `name: string`

    The name of the folder.

  - `created_at?: string | null`

    The timestamp when the folder was created.

  - `created_by_id?: string | null`

    The id of the user that made this Tool.

  - `description?: string | null`

    The description of the folder.

  - `instructions?: string | null`

    Instructions for how to use the folder.

  - `last_updated_by_id?: string | null`

    The id of the user that made this Tool.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the folder.

  - `updated_at?: string | null`

    The timestamp when the folder was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const folder of client.folders.list()) {
  console.log(folder.id);
}
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

`client.folders.create(FolderCreateParamsbody, RequestOptionsoptions?): Folder`

**post** `/v1/folders/`

Create a new data folder.

### Parameters

- `body: FolderCreateParams`

  - `name: string`

    The name of the source.

  - `description?: string | null`

    The description of the source.

  - `embedding?: string | null`

    The handle for the embedding config used by the source.

  - `embedding_chunk_size?: number | null`

    The chunk size of the embedding.

  - `embedding_config?: EmbeddingConfig | null`

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

  - `instructions?: string | null`

    Instructions for how to use the source.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the source.

### Returns

- `Folder`

  Representation of a folder, which is a collection of files and passages.

  - `id: string`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

  - `name: string`

    The name of the folder.

  - `created_at?: string | null`

    The timestamp when the folder was created.

  - `created_by_id?: string | null`

    The id of the user that made this Tool.

  - `description?: string | null`

    The description of the folder.

  - `instructions?: string | null`

    Instructions for how to use the folder.

  - `last_updated_by_id?: string | null`

    The id of the user that made this Tool.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the folder.

  - `updated_at?: string | null`

    The timestamp when the folder was last updated.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const folder = await client.folders.create({ name: 'name' });

console.log(folder.id);
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

- `Folder`

  Representation of a folder, which is a collection of files and passages.

  - `id: string`

    The human-friendly ID of the Source

  - `embedding_config: EmbeddingConfig`

    The embedding configuration used by the folder.

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

  - `name: string`

    The name of the folder.

  - `created_at?: string | null`

    The timestamp when the folder was created.

  - `created_by_id?: string | null`

    The id of the user that made this Tool.

  - `description?: string | null`

    The description of the folder.

  - `instructions?: string | null`

    Instructions for how to use the folder.

  - `last_updated_by_id?: string | null`

    The id of the user that made this Tool.

  - `metadata?: Record<string, unknown> | null`

    Metadata associated with the folder.

  - `updated_at?: string | null`

    The timestamp when the folder was last updated.

### Folder Delete Response

- `FolderDeleteResponse = unknown`

# Files

## Upload File To Folder

`client.folders.files.upload(stringfolderID, FileUploadParamsparams, RequestOptionsoptions?): FileUploadResponse`

**post** `/v1/folders/{folder_id}/upload`

Upload a file to a data folder.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

- `params: FileUploadParams`

  - `file: Uploadable`

    Body param

  - `duplicate_handling?: "skip" | "error" | "suffix" | "replace"`

    Query param: How to handle duplicate filenames

    - `"skip"`

    - `"error"`

    - `"suffix"`

    - `"replace"`

  - `name?: string | null`

    Query param: Optional custom name to override the uploaded file's name

### Returns

- `FileUploadResponse`

  Representation of a single FileMetadata

  - `id: string`

    The human-friendly ID of the File

  - `source_id: string`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded?: number | null`

    Number of chunks that have been embedded.

  - `content?: string | null`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at?: string | null`

    The creation date of the file.

  - `error_message?: string | null`

    Optional error message if the file failed processing.

  - `file_creation_date?: string | null`

    The creation date of the file.

  - `file_last_modified_date?: string | null`

    The last modified date of the file.

  - `file_name?: string | null`

    The name of the file.

  - `file_path?: string | null`

    The path to the file.

  - `file_size?: number | null`

    The size of the file in bytes.

  - `file_type?: string | null`

    The type of the file (MIME type).

  - `original_file_name?: string | null`

    The original name of the file as uploaded.

  - `processing_status?: "pending" | "parsing" | "embedding" | 2 more`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks?: number | null`

    Total number of chunks for the file.

  - `updated_at?: string | null`

    The update date of the file.

### Example

```typescript
import fs from 'fs';
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const response = await client.folders.files.upload('source-123e4567-e89b-42d3-8456-426614174000', {
  file: fs.createReadStream('path/to/file'),
});

console.log(response.id);
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

`client.folders.files.list(stringfolderID, FileListParamsquery?, RequestOptionsoptions?): ArrayPage<FileListResponse>`

**get** `/v1/folders/{folder_id}/files`

List paginated files associated with a data folder.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

- `query: FileListParams`

  - `after?: string | null`

    Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (file ID). Returns results relative to this ID in the specified sort order. Expected format: 'file-<uuid4>'

  - `include_content?: boolean`

    Whether to include full file content

  - `limit?: number | null`

    Maximum number of files to return

  - `order?: "asc" | "desc"`

    Sort order for files by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `FileListResponse`

  Representation of a single FileMetadata

  - `id: string`

    The human-friendly ID of the File

  - `source_id: string`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded?: number | null`

    Number of chunks that have been embedded.

  - `content?: string | null`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at?: string | null`

    The creation date of the file.

  - `error_message?: string | null`

    Optional error message if the file failed processing.

  - `file_creation_date?: string | null`

    The creation date of the file.

  - `file_last_modified_date?: string | null`

    The last modified date of the file.

  - `file_name?: string | null`

    The name of the file.

  - `file_path?: string | null`

    The path to the file.

  - `file_size?: number | null`

    The size of the file in bytes.

  - `file_type?: string | null`

    The type of the file (MIME type).

  - `original_file_name?: string | null`

    The original name of the file as uploaded.

  - `processing_status?: "pending" | "parsing" | "embedding" | 2 more`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks?: number | null`

    Total number of chunks for the file.

  - `updated_at?: string | null`

    The update date of the file.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

// Automatically fetches more pages as needed.
for await (const fileListResponse of client.folders.files.list(
  'source-123e4567-e89b-42d3-8456-426614174000',
)) {
  console.log(fileListResponse.id);
}
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

`client.folders.files.retrieve(stringfileID, FileRetrieveParamsparams, RequestOptionsoptions?): FileRetrieveResponse`

**get** `/v1/folders/{folder_id}/files/{file_id}`

Retrieve a file from a folder by ID.

### Parameters

- `fileID: string`

  The ID of the file in the format 'file-<uuid4>'

- `params: FileRetrieveParams`

  - `folder_id: string`

    Path param: The ID of the source in the format 'source-<uuid4>'

  - `include_content?: boolean`

    Query param: Whether to include full file content

### Returns

- `FileRetrieveResponse`

  Representation of a single FileMetadata

  - `id: string`

    The human-friendly ID of the File

  - `source_id: string`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded?: number | null`

    Number of chunks that have been embedded.

  - `content?: string | null`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at?: string | null`

    The creation date of the file.

  - `error_message?: string | null`

    Optional error message if the file failed processing.

  - `file_creation_date?: string | null`

    The creation date of the file.

  - `file_last_modified_date?: string | null`

    The last modified date of the file.

  - `file_name?: string | null`

    The name of the file.

  - `file_path?: string | null`

    The path to the file.

  - `file_size?: number | null`

    The size of the file in bytes.

  - `file_type?: string | null`

    The type of the file (MIME type).

  - `original_file_name?: string | null`

    The original name of the file as uploaded.

  - `processing_status?: "pending" | "parsing" | "embedding" | 2 more`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks?: number | null`

    Total number of chunks for the file.

  - `updated_at?: string | null`

    The update date of the file.

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const file = await client.folders.files.retrieve('file-123e4567-e89b-42d3-8456-426614174000', {
  folder_id: 'source-123e4567-e89b-42d3-8456-426614174000',
});

console.log(file.id);
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

`client.folders.files.delete(stringfileID, FileDeleteParamsparams, RequestOptionsoptions?): void`

**delete** `/v1/folders/{folder_id}/{file_id}`

Delete a file from a folder.

### Parameters

- `fileID: string`

  The ID of the file in the format 'file-<uuid4>'

- `params: FileDeleteParams`

  - `folder_id: string`

    The ID of the source in the format 'source-<uuid4>'

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

await client.folders.files.delete('file-123e4567-e89b-42d3-8456-426614174000', {
  folder_id: 'source-123e4567-e89b-42d3-8456-426614174000',
});
```

## Domain Types

### File Upload Response

- `FileUploadResponse`

  Representation of a single FileMetadata

  - `id: string`

    The human-friendly ID of the File

  - `source_id: string`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded?: number | null`

    Number of chunks that have been embedded.

  - `content?: string | null`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at?: string | null`

    The creation date of the file.

  - `error_message?: string | null`

    Optional error message if the file failed processing.

  - `file_creation_date?: string | null`

    The creation date of the file.

  - `file_last_modified_date?: string | null`

    The last modified date of the file.

  - `file_name?: string | null`

    The name of the file.

  - `file_path?: string | null`

    The path to the file.

  - `file_size?: number | null`

    The size of the file in bytes.

  - `file_type?: string | null`

    The type of the file (MIME type).

  - `original_file_name?: string | null`

    The original name of the file as uploaded.

  - `processing_status?: "pending" | "parsing" | "embedding" | 2 more`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks?: number | null`

    Total number of chunks for the file.

  - `updated_at?: string | null`

    The update date of the file.

### File List Response

- `FileListResponse`

  Representation of a single FileMetadata

  - `id: string`

    The human-friendly ID of the File

  - `source_id: string`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded?: number | null`

    Number of chunks that have been embedded.

  - `content?: string | null`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at?: string | null`

    The creation date of the file.

  - `error_message?: string | null`

    Optional error message if the file failed processing.

  - `file_creation_date?: string | null`

    The creation date of the file.

  - `file_last_modified_date?: string | null`

    The last modified date of the file.

  - `file_name?: string | null`

    The name of the file.

  - `file_path?: string | null`

    The path to the file.

  - `file_size?: number | null`

    The size of the file in bytes.

  - `file_type?: string | null`

    The type of the file (MIME type).

  - `original_file_name?: string | null`

    The original name of the file as uploaded.

  - `processing_status?: "pending" | "parsing" | "embedding" | 2 more`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks?: number | null`

    Total number of chunks for the file.

  - `updated_at?: string | null`

    The update date of the file.

### File Retrieve Response

- `FileRetrieveResponse`

  Representation of a single FileMetadata

  - `id: string`

    The human-friendly ID of the File

  - `source_id: string`

    Deprecated: Use `folder_id` field instead. The unique identifier of the source associated with the document.

  - `chunks_embedded?: number | null`

    Number of chunks that have been embedded.

  - `content?: string | null`

    Optional full-text content of the file; only populated on demand due to its size.

  - `created_at?: string | null`

    The creation date of the file.

  - `error_message?: string | null`

    Optional error message if the file failed processing.

  - `file_creation_date?: string | null`

    The creation date of the file.

  - `file_last_modified_date?: string | null`

    The last modified date of the file.

  - `file_name?: string | null`

    The name of the file.

  - `file_path?: string | null`

    The path to the file.

  - `file_size?: number | null`

    The size of the file in bytes.

  - `file_type?: string | null`

    The type of the file (MIME type).

  - `original_file_name?: string | null`

    The original name of the file as uploaded.

  - `processing_status?: "pending" | "parsing" | "embedding" | 2 more`

    The current processing status of the file (e.g. pending, parsing, embedding, completed, error).

    - `"pending"`

    - `"parsing"`

    - `"embedding"`

    - `"completed"`

    - `"error"`

  - `total_chunks?: number | null`

    Total number of chunks for the file.

  - `updated_at?: string | null`

    The update date of the file.

# Agents

## List Agents For Folder

`client.folders.agents.list(stringfolderID, AgentListParamsquery?, RequestOptionsoptions?): AgentListResponse`

**get** `/v1/folders/{folder_id}/agents`

Get all agent IDs that have the specified folder attached.

### Parameters

- `folderID: string`

  The ID of the source in the format 'source-<uuid4>'

- `query: AgentListParams`

  - `after?: string | null`

    Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

  - `before?: string | null`

    Cursor for pagination (agent ID). Returns results relative to this ID in the specified sort order. Expected format: 'agent-<uuid4>'

  - `limit?: number | null`

    Maximum number of agents to return

  - `order?: "asc" | "desc"`

    Sort order for agents by creation time. 'asc' for oldest first, 'desc' for newest first

    - `"asc"`

    - `"desc"`

  - `order_by?: "created_at"`

    Field to sort by

    - `"created_at"`

### Returns

- `AgentListResponse = Array<string>`

### Example

```typescript
import Letta from '@letta-ai/letta-client';

const client = new Letta({
  apiKey: process.env['LETTA_API_KEY'], // This is the default and can be omitted
});

const agents = await client.folders.agents.list('source-123e4567-e89b-42d3-8456-426614174000');

console.log(agents);
```

#### Response

```json
[
  "string"
]
```

## Domain Types

### Agent List Response

- `AgentListResponse = Array<string>`
