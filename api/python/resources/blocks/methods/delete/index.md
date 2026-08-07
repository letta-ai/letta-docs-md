## Delete Block

`blocks.delete(strblock_id)  -> object`

**delete** `/v1/blocks/{block_id}`

Delete Block

### Parameters

- `block_id: str`

  The ID of the block in the format 'block-<uuid4>'

### Returns

- `object`

### Example

```python
import os
from letta_client import Letta

client = Letta(
    api_key=os.environ.get("LETTA_API_KEY"),  # This is the default and can be omitted
)
block = client.blocks.delete(
    "block-123e4567-e89b-42d3-8456-426614174000",
)
print(block)
```

#### Response

```json
{}
```
