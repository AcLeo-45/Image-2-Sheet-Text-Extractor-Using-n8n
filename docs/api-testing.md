# API Testing Guide

## Using External API Testing Tools

### With reqbin.com

1. Go to reqbin.com
2. Set method to **POST**
3. Enter your n8n webhook URL
4. In the request body, use this JSON format:
```json
{
  "body": {
    "imageUrl": "https://via.placeholder.com/300x200/000000/FFFFFF?text=Sample+Text"
  }
}
