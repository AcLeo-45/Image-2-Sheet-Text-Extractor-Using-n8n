# Image OCR to Google Sheets Automation

An automated workflow that extracts text from image URLs using OCR.space API and saves the results to Google Sheets.

## Overview

This project uses a 6-node workflow to:
- Receive image URLs via webhook
- Download and process images
- Extract text using OCR.space API
- Save extracted text to Google Sheets

## Features

- ✅ Webhook-based image URL input
- ✅ Automatic image download
- ✅ OCR text extraction using OCR.space
- ✅ Google Sheets integration
- ✅ Process tracking with timestamps
- ✅ Status monitoring

## Quick Start

1. Set up the workflow nodes as described in `/docs/workflow-setup.md`
2. Configure your OCR.space API key
3. Connect your Google Sheets
4. Test with the webhook URL

## Workflow Nodes

1. Webhook Trigger - Receives POST requests with image URLs
2. Prepare Image Data - Maps and validates image URL
3. Download Image - Fetches image from URL
4. OCR Text Extraction - Extracts text using OCR.space
5. Process Extracted Text - Formats and validates results
6. Save to Google Sheets - Stores data in spreadsheet

## Documentation

- [Detailed Setup Guide](docs/workflow-setup.md)
- [API Testing Guide](docs/api-testing.md)
- [Troubleshooting](docs/troubleshooting.md)

## Requirements

- n8n workflow automation tool
- OCR.space API account (free tier available)
- Google Sheets access
- External API testing tool (like reqbin.com)
