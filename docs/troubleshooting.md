# Troubleshooting Guide

Image Download Issues
Problem: "Failed to download image"

Solution: Verify the image URL is publicly accessible
Check: Test the image URL directly in a browser
Note: Some websites block automated downloads

Problem: Image format not supported

Solution: Use common formats (PNG, JPG, JPEG, GIF)
Alternative: Convert image to PNG format

OCR Issues
Problem: "No text found" result

Solution: Ensure image contains readable text
Check: Image quality and resolution
Verify: Text is not too small or blurry

Problem: OCR API rate limit exceeded

Solution: Wait a few minutes before retrying
Alternative: Consider upgrading to OCR.space paid plan
Check: API key is valid ("helloworld" for free tier)

Google Sheets Issues
Problem: Authentication failed

Solution: Reconnect your Google Sheets credentials in n8n
Check: Google Sheets API permissions

Problem: Data not appearing in sheet

Solution: Verify sheet URL and column headers match exactly:

Timestamp
Process ID
Image URL
Extracted Text
OCR Status



Problem: "Sheet not found" error

Solution: Ensure the Google Sheet is accessible and shared properly
Check: Sheet ID in the URL is correct

General Debugging
Enable Debug Mode:

In n8n workflow, click on each node
Check the execution data and error messages
Look for JSON structure mismatches

Check Node Connections:

Ensure all nodes are properly connected
Verify data is flowing between nodes correctly

Test Individual Nodes:

Use the "Execute Node" feature to test each step
Check intermediate results

Error Codes

OCRExitCode = 1: Success
OCRExitCode = 2: Parsing failed
OCRExitCode = 3: File format error
OCRExitCode = 4: API limit exceeded

Support
If you encounter issues not covered here:

Check n8n execution logs
Verify all API keys and credentials
Test with simple image URLs first
Review the workflow configuration step by step
---------------------------------------------------------------------------------


# Common Issues and Solutions

### Webhook Issues

**Problem**: Webhook not triggering
- **Solution**: Check if the webhook URL is correct and accessible
- **Check**: Ensure the HTTP method is set to POST
- **Verify**: Test the webhook URL directly in a browser (should show n8n webhook page)

**Problem**: "Cannot read property 'imageUrl' of undefined"
- **Solution**: Ensure your request body uses the correct format:
```json
{
  "body": {
    "imageUrl": "your-image-url-here"
  }
}
