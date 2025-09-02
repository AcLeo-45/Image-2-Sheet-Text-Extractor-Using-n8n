# Workflow Setup Guide

This guide provides detailed instructions for setting up each node in the OCR workflow.

## Prerequisites

- n8n installed and running
- OCR.space API key (free tier: "helloworld")
- Google Sheets document with 5 columns: Timestamp, Process ID, Image URL, Extracted Text, OCR Status
- External API testing tool access (reqbin.com)

## Node Configuration Details

### Node 1: Webhook Trigger
### Node 2: Prepare Image Data  
### Node 3: Download Image
### Node 4: OCR Text Extraction
### Node 5: Process Extracted Text
### Node 6: Save to Google Sheets


### Node 1: Webhook Trigger
- Type: Webhook
- HTTP Method: POST
- Path: Auto-generated (e.g., `897a23f5-7777-56c0-5050-2ee1234d6789`)
- Authentication: None
- Response Mode: When Last Node Finishes
- Options: Default settings

### Node 2: Prepare Image Data
- Type: Set (Edit Fields)
- Mode: Manual Mapping
- Assignments:
  - Name: `originalImageUrl`
  - Value: `{{ $json.body.imageUrl }}` (Note: accessing via body.imageUrl)
  - Type: String

### Note: The webhook expects the image URL to be nested under body.imageUrl, not directly as imageUrl

### Node 3: Download Image
- Type: HTTP Request
- Method: GET
- URL: `{{ $json.originalImageUrl }}`
- Authentication: None
- Response Options:
  - Response Format: File
  - Output Property Name: `imageFile`

### Node 4: OCR Text Extraction
- Type: HTTP Request
- Method: POST
- URL: `https://api.ocr.space/parse/image`
- Send Headers: Yes
- Header Parameters:
  - apikey: `helloworld`
  - Content-Type: `multipart/form-data`
- Send Body: Yes
- Content Type: multipart-form-data
- Body Parameters:
  - Parameter 1:
    - Type: Form Binary Data
    - Name: `file`
    - Input Data Field Name: `imageFile`
  - Parameter 2:
    - Type: Form Data
    - Name: `filetype`
    - Value: `PNG`

### Node 5: Process Extracted Text
- Type: Set (Edit Fields)
- Assignments:
  - extractedText: `{{ $json.ParsedResults && $json.ParsedResults[0] ? $json.ParsedResults[0].ParsedText.trim() : 'No text found' }}`
  - ocrSuccess: `{{ $json.OCRExitCode === 1 ? 'Success' : 'Failed' }}`
  - imageUrl: `{{ $('Prepare Image Data').item.json.originalImageUrl }}`
  - timestamp: `{{ new Date().toLocaleString() }}`
  - processId: `{{ Math.random().toString(36).substr(2, 9) }}`

### Node 6: Save to Google Sheets
- Type: Google Sheets
- Authentication: Connect your Google account
- Operation: Append
- Document: Your Google Sheets URL (via URL mode)
- Sheet: Select your sheet (gid=0 for Sheet1)
- Columns Mapping Mode: Define Below
- Column Mappings:
  - Timestamp: `{{ $json.timestamp }}`
  - Process ID: `{{ $json.processId }}`
  - Image URL: `{{ $json.imageUrl }}`
  - Extracted Text: `{{ $json.extractedText }}`
  - OCR Status: `{{ $json.ocrSuccess }}`

## Google Sheets Setup

Create a spreadsheet with these exact column headers:
1. Timestamp
2. Process ID
3. Image URL 
4. Extracted Text
5. OCR Status

## Request Format for Testing

When testing via reqbin.com or other API tools, use this JSON structure:
```json
{
  "body": {
    "imageUrl": "https://example.com/path/to/your/image.png"
  }
}
