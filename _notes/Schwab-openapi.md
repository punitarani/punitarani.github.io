---
layout: post
title: Download the Schwab OpenAPI Spec
permalink: schwab/openapi-spec
author: Punit Arani
date: July 8, 2024
summary: Downloading the Schwab OpenAPI spec.
category: Quant
---

> You need access to Schwab API to get the OpenAPI spec.

1. Login and go to `https://developer.schwab.com/products/trader-api--individual/details/specifications/Market%20Data%20Production`
2. Open Dev Tools and go to Network tab (refresh the page if needed)
3. Look for a request names `Market%20Data%20Production`

The response is a JSON object with the following structure:

```JSON
{
    "id": "123",
    "apiName": "Market Data Production",
    "fileName": "TraderApi.json",
    "specification": "{\r\n  \"openapi\": \"3.0.3\" ...",
    "appKey": "key",
    "appSecret": "secret"
}
```

## Parsing the JSON

```Python
import json

specification: "{\r\n  \"openapi\": \"3.0.3\" ...",
openapi_spec = json.loads(specification)

with open("schwab-openapi.json", "w") as f:
    json.dump(openapi_spec, f, indent=2)
```

## Generating Pydantic Models

Install [`datamodel-code-generator`](https://docs.pydantic.dev/latest/integrations/datamodel_code_generator/)

```Bash
pip install datamodel-code-generator
```

Run the following command to generate Pydantic models:

````Bash

```bash
datamodel-codegen  --input schwab-openapi.json --input-file-type openapi --output models.py --output-model-type pydantic_v2.BaseModel
````
