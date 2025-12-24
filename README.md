# LLM Chat API (Cloudflare Workers AI)

A secure, API-only LLM endpoint powered by Cloudflare Workers AI. 

> **Note:** This is an API-only deployment. No public web interface - all endpoints require authentication.

## Features

- 🔐 **API Key Authentication** - All requests require Bearer token
- ⚡ **Server-Sent Events (SSE)** - Real-time streaming responses
- 🧠 **Llama 3.1 8B** - Fast, high-quality responses via Cloudflare edge
- 🌍 **Global Edge Network** - Low latency worldwide

## API Usage

### Endpoint

```
POST /api/chat
```

### Headers

```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

### Request Body

```json
{
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello!"}
  ]
}
```

### Response

Server-Sent Events stream:

```
data: {"response":"Hello"}
data: {"response":"!"}
data: {"response":" How"}
data: {"response":" can I help?"}
data: [DONE]
```

## Deployment

### Prerequisites

- Node.js v18+
- Cloudflare account with Workers AI access
- [Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install-and-update/)

### Setup

1. Clone and install:
   ```bash
   git clone https://github.com/not-antoni/llm-chat-app-template.git
   cd llm-chat-app-template
   npm install
   ```

2. Deploy:
   ```bash
   npx wrangler deploy
   ```

3. Set your API key secret:
   ```bash
   npx wrangler secret put API_KEY
   # Enter your secret API key when prompted
   ```

## Security

- **No public access** - Root URL returns `403 Access denied`
- **API key required** - Invalid/missing key returns `401 Unauthorized`
- **Secrets stored in Cloudflare** - Not in the repository

## Rate Limits

- Free tier: 10,000 tokens/day
- Rate limit: 300 requests/minute

## Resources

- [Cloudflare Workers AI Docs](https://developers.cloudflare.com/workers-ai/)
- [Available Models](https://developers.cloudflare.com/workers-ai/models/)
