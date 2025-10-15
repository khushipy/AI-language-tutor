# AI Language Tutor Setup Guide

## Prerequisites

1. Node.js (v14 or later)
2. npm (comes with Node.js)
3. Google Cloud Platform account
4. OpenAI API key
5. n8n (will be installed locally)

## Installation

1. Clone this repository
2. Install dependencies:
   ```bash
   npm install
   ```

## Google Cloud Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable the following APIs:
   - Google Sheets API
   - Google Cloud Text-to-Speech API
4. Create OAuth 2.0 credentials:
   - Go to APIs & Services > Credentials
   - Click "Create Credentials" > "OAuth client ID"
   - Select "Web application"
   - Add authorized redirect URIs:
     - `http://localhost:5678/rest/oauth2-credential/callback`
   - Download the credentials JSON file

## Google Sheets Setup

1. Create a new Google Sheet
2. Create two sheets:
   - "Users" - for storing user information
     - Columns: userId, nativeLanguage, targetLanguage, learningTopic, aiPersonality, createdAt
   - "Conversations" - for storing chat history
     - Columns: userId, role (user/assistant), message, timestamp
3. Share the sheet with the service account email from your Google Cloud project

## OpenAI Setup

1. Get an API key from [OpenAI](https://platform.openai.com/account/api-keys)
2. Keep it secure and don't commit it to version control

## n8n Setup

1. Start n8n:
   ```bash
   npx n8n start
   ```
2. Access the n8n web interface at `http://localhost:5678`
3. Set up credentials:
   - Google Sheets OAuth2 API
   - Google Cloud Text-to-Speech OAuth2 API
   - OpenAI API

## Import Workflows

1. In n8n, go to "Workflows" > "Import from File"
2. Import both workflow JSON files from the `workflows/` directory
3. Update the following in each workflow:
   - Replace `YOUR_GOOGLE_SHEET_ID` with your actual Google Sheet ID
   - Configure the OpenAI node with your API key
   - Set up the Google Cloud Text-to-Speech node with your GCP credentials

## Testing the Workflows

### Test User Onboarding

Send a POST request to:
```
http://localhost:5678/webhook/user-onboarding
```

With JSON body:
```json
{
  "userId": "user123",
  "nativeLanguage": "English",
  "targetLanguage": "Spanish",
  "learningTopic": "Travel Phrases",
  "aiPersonality": "friendly"
}
```

### Test Chat

Send a POST request to:
```
http://localhost:5678/webhook/chat
```

With JSON body:
```json
{
  "userId": "user123",
  "message": "How do you say 'Hello, how are you?' in Spanish?"
}
```

## Deployment

For production use, consider deploying n8n to a cloud provider like:
- n8n.cloud
- Heroku
- DigitalOcean
- AWS

Make sure to:
1. Set up proper authentication
2. Use environment variables for sensitive information
3. Set up monitoring and logging
4. Configure HTTPS
