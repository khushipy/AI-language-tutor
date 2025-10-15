# AI Language Tutor with n8n

This project implements a two-part AI language tutoring system using n8n workflows.

## Workflows

### 1. User Onboarding Workflow
- **Trigger**: Webhook
- **Actions**:
  - Accepts user ID, native language, target language, learning topic, and AI personality
  - Saves preferences to Google Sheets

### 2. Conversational Tutor Workflow
- **Trigger**: Webhook with user ID and message
- **Actions**:
  - Fetches user preferences and chat history
  - Generates AI response using a smart prompt
  - Saves conversation to database
  - Converts response to speech
  - Returns audio file

## Setup

1. Install dependencies:
   ```bash
   npm install
   ```

2. Start n8n:
   ```bash
   npx n8n start
   ```

3. Import the workflow JSON files from the `workflows/` directory into your n8n instance.
