# Obelis Redeploy GitHub Action

This GitHub Action allows you to trigger a redeploy of your Obelis project directly from your GitHub workflows.

## Usage

### Basic Usage

```yaml
- name: Redeploy Project
  uses: ObelisAI/redeploy
  with:
    project_id: 'your-project-id'
    api_key: ${{ secrets.OBELIS_API_KEY }}
```

### Complete Example

```yaml
name: Redeploy on Push

on:
  push:
    branches: [ main ]

jobs:
  redeploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Redeploy Project
        uses: ObelisAI/redeploy
        with:
          project_id: 'your-project-id'
          api_key: ${{ secrets.OBELIS_API_KEY }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `project_id` | The ID of the Obelis project to redeploy | Yes | - |
| `api_key` | The Obelis API key for authentication | Yes | - |

## Outputs

| Output | Description |
|--------|-------------|
| `status` | HTTP status code of the API response |
| `response` | Full response body from the API |
| `success` | Boolean indicating if the redeploy was initiated successfully |

## Setup

### 1. Get Your Project ID

You can find your project ID in your Obelis AI project details.

### 2. Create API Key

1. Go to your Obelis AI dashboard
2. Navigate to Account Settings → API Keys
3. Create a new API key
4. Copy the key value

### 3. Add GitHub Secret

1. Go to your GitHub repository
2. Navigate to Settings → Secrets and variables → Actions
3. Create a new repository secret named `OBELIS_API_KEY`
4. Paste your API key as the value

### 4. Use the Action

Add the action to your workflow as shown in the usage examples above.

## Error Handling

The action will:
- ✅ Succeed if the redeploy is initiated successfully (HTTP 2xx)
- ❌ Fail if the API call fails (non-2xx status codes)
- Always output the full API response for debugging

## Security

- The API base URL is hardcoded and not exposed to users
- API keys should always be stored as GitHub secrets
- The action uses secure authentication via the `X-API-Key` header

## Troubleshooting

### Common Issues

1. **Invalid API Key**: Ensure your API key is correct and has the necessary permissions
2. **Invalid Project ID**: Verify the project ID exists and belongs to your account
3. **Network Issues**: Check your GitHub Actions runner's network connectivity

### Debug Output

The action provides detailed output including:
- HTTP status code
- Full API response body
- Success/failure status

This information can help diagnose any issues with the redeploy request. 