# Agentic Honey-Pot System - User Guide

## Overview

The Agentic Honey-Pot System is a demonstration of an AI-powered scam detection and intelligence extraction platform. This system can:

- **Detect scam messages** with high accuracy using pattern matching and machine learning heuristics
- **Deploy AI agents** that engage scammers in human-like conversations
- **Extract intelligence** including UPI IDs, bank accounts, phishing links, and phone numbers
- **Provide API interface** for integration with messaging platforms

## Features

### 1. Dashboard
- Real-time monitoring of active scam detection sessions
- Statistics on total sessions, active scams, and intelligence extracted
- Average confidence scoring across all detections
- Quick access to individual session details

### 2. Conversation Simulator
- Interactive conversation testing with simulated scammers
- Multi-turn dialogue support
- Real-time scam detection during conversations
- Automatic AI agent response generation
- Session management with status tracking

### 3. Intelligence Viewer
- Comprehensive display of extracted intelligence data
- Categorized display of:
  - UPI IDs
  - Bank account numbers
  - Phishing links
  - Phone numbers
  - Suspicious keywords
- Copy-to-clipboard functionality for all extracted data
- JSON export for further analysis
- Agent analysis notes

### 4. API Tester
- Test API endpoint with custom requests
- Pre-loaded example scenarios
- Real-time request/response visualization
- API documentation reference
- Support for both first messages and follow-up messages

## How to Use

### Testing Scam Detection

1. **Navigate to the Conversation tab**
2. Select a channel (SMS, WhatsApp, Email, Chat)
3. Enter a scammer message in the text area
4. Click "Send" to trigger AI agent response
5. Continue the conversation to extract maximum intelligence

### Example Scam Messages to Test:

```
"Your bank account will be blocked today. Verify immediately."

"Congratulations! You won ₹50,000. Send ₹500 processing fee to claim."

"Update your KYC details now or your account will be suspended."

"Click this link to verify your payment: http://fake-bank.com"
```

### Viewing Intelligence Reports

1. **Go to the Dashboard**
2. Click "View Details" on any active session
3. Navigate to the **Intelligence** tab
4. Review all extracted data:
   - UPI IDs and bank accounts
   - Phishing links
   - Phone numbers
   - Suspicious keywords
5. Use the "Export JSON" button to download the full report

### API Testing

1. **Navigate to the API Tester tab**
2. Load a pre-defined example or create your own JSON request
3. Modify the request payload as needed
4. Click "Test API" to process the request
5. View the AI agent's response in the Response panel

## API Specification

### Request Format

```json
{
  "sessionId": "unique-session-id",
  "message": {
    "sender": "scammer",
    "text": "Message text here",
    "timestamp": 1770005528731
  },
  "conversationHistory": [],
  "metadata": {
    "channel": "SMS",
    "language": "English",
    "locale": "IN"
  }
}
```

### Response Format

```json
{
  "status": "success",
  "reply": "AI agent response text",
  "scamDetected": true,
  "confidence": 0.85
}
```

### Final Result Callback

When a conversation ends, the system sends this payload to the evaluation endpoint:

```json
{
  "sessionId": "abc123-session-id",
  "scamDetected": true,
  "totalMessagesExchanged": 18,
  "extractedIntelligence": {
    "bankAccounts": ["XXXX-XXXX-XXXX"],
    "upiIds": ["scammer@upi"],
    "phishingLinks": ["http://malicious-link.example"],
    "phoneNumbers": ["+91XXXXXXXXXX"],
    "suspiciousKeywords": ["urgent", "verify now", "account blocked"]
  },
  "agentNotes": "Scammer used urgency tactics and payment redirection"
}
```

## Scam Detection Algorithm

The system uses multiple detection methods:

### Pattern Matching
- **Urgency indicators**: "urgent", "immediately", "now", "today"
- **Threats**: "block", "suspend", "legal action", "arrest"
- **Financial keywords**: "bank account", "upi", "payment", "refund"
- **Verification requests**: "verify", "confirm", "update", "kyc"
- **Information requests**: "share", "send", "password", "otp"

### Regex Patterns
- Phone numbers: `\b\d{10,}\b`
- URLs: `https?://[^\s]+`
- UPI IDs: `[\w.-]+@[\w]+`
- Card numbers: `\d{4}[-\s]?\d{4}[-\s]?\d{4}[-\s]?\d{4}`
- Bank accounts: `\b\d{9,18}\b`

### Confidence Scoring
- Each matched pattern adds to the confidence score
- Threshold: 40% confidence = scam detected
- Higher scores indicate more certain scam detection

## AI Agent Behavior

The AI agent uses multiple personas:

### Personas
1. **Cautious Senior** - Elderly, confused, asking basic questions
2. **Busy Professional** - Impatient, tech-savvy, asking for verification
3. **Naive User** - Trusting, eager to help, easily manipulated

### Response Strategy
- Initial responses show confusion or concern
- Curious responses ask clarifying questions
- Hesitant responses express doubt
- Cooperative responses show willingness (to extract more info)
- Technical responses ask about processes

### Intelligence Extraction
The agent strategically asks questions to extract:
- Contact information
- Payment details
- Website links
- Official company information
- Verification processes

## Data Storage

All session data is stored in browser localStorage:
- Session history
- Conversation messages
- Extracted intelligence
- Agent notes

To clear data: Open browser developer console and run:
```javascript
localStorage.removeItem('honeypot_sessions');
```

## Best Practices

1. **Let conversations run long enough** - The AI agent needs 5-8 messages to extract maximum intelligence
2. **Test different scam types** - Prize scams, banking fraud, KYC scams, phishing
3. **Monitor confidence scores** - Higher scores indicate clearer scam patterns
4. **Review agent notes** - Provides insights into scammer tactics
5. **Export intelligence data** - Save reports for analysis and documentation

## Limitations

This is a **demonstration system** for educational purposes:
- Does not connect to real LLM APIs
- Uses rule-based AI agent responses
- Does not make actual API calls to external endpoints
- Stores data only in browser localStorage
- Not designed for production deployment

## Future Enhancements

For a production system, consider:
- Integration with real LLM APIs (GPT-4, Claude, etc.)
- Backend database for persistent storage
- Real-time API webhook support
- Advanced machine learning models for detection
- Multi-language support
- Reporting and analytics dashboard
- Integration with telecom and messaging platforms

## Security & Ethics

⚠️ **Important Considerations**:
- ❌ Do not use to impersonate real individuals
- ❌ Do not deploy without proper legal authorization
- ❌ Do not use for harassment or illegal activities
- ✅ Handle extracted data responsibly
- ✅ Follow data protection regulations
- ✅ Use only for legitimate scam prevention

## Support

For questions or issues with this demonstration:
1. Review this documentation
2. Check the API Tester for example payloads
3. Examine the conversation simulator for behavior examples
4. Review the code in `/src/app/utils/` for algorithm details

---

**Built for GUVI Hackathon Challenge**
*Agentic Honey-Pot for Scam Detection & Intelligence Extraction*
