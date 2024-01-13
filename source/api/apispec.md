# API Specification

[Download OpenAPI Specification](./spec.yaml)

**URL**: `https://contextcrunch.com/api/call`

**Method**: `POST`

## Request Body

| Field               | Type    | Required | Description                               | Constraints         |
|---------------------|---------|----------|-------------------------------------------|---------------------|
| `context`           | string  | Yes      | This is some context                      |                     |
| `prompt`            | string  | Yes      | This is a question about the context      |                     |
| `type`              | string  | No       | Type of request, 'conversation' or 'rag'  | Default: `rag`      |
| `compression_ratio` | number  | No       | Compression ratio                         | 0.5 < x < 1.0, Default: 0.9 |

## Responses

- `200 OK`: Successful response with output data.
- `400 Bad Request`: No input provided.
- `401 Unauthorized`: Invalid API key.
- `402 Payment Required`: Insufficient balance on your account.
- `500 Internal Server Error`: Something went wrong on our end! Contact [info@contextcrunch.com](mailto:info@contextcrunch.com)

### Response Structure

| Field            | Type    | Description                       |
|------------------|---------|-----------------------------------|
| `output`         | string  | The response output               |
| `tokensCharged`  | integer | The number of tokens charged      |
| `outputTokens`   | integer | The number of tokens in the output|