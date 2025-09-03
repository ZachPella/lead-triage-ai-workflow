# LedgerLift Lead Triage Agent

An intelligent AI-powered lead triage system built with n8n that automatically processes, categorizes, and routes inbound leads from Google Sheets.

## Overview

This AI agent automatically:
- **Monitors** new leads added to a Google Sheet
- **Categorizes** leads by type (demo, security, support, pricing, sales, spam)
- **Prioritizes** leads (high, medium, low, spam)
- **Routes** leads to appropriate team members
- **Creates** email drafts for responses
- **Updates** the lead database with processing results

## Features

- 🔄 **Real-time Processing**: Monitors Google Sheets for new lead entries
- 🎯 **Smart Categorization**: Uses AI to classify leads into relevant categories
- 📊 **Priority Assessment**: Automatically assigns priority levels based on content analysis
- 👥 **Team Routing**: Routes leads to appropriate team members based on category
- 📧 **Email Automation**: Creates contextual email drafts for both internal handoffs and prospect responses
- 🛡️ **Spam Detection**: Identifies and filters out irrelevant or promotional content

## Architecture

### Core Components

1. **Google Sheets Trigger**: Monitors the "Leads Database" sheet for new entries
2. **Lead Triage Agent**: AI-powered agent that processes and categorizes leads
3. **Google Sheets Tools**: Updates lead records and looks up team routing information
4. **Gmail Integration**: Creates email drafts based on lead category and context

### Data Flow

```
New Lead → Google Sheets → AI Agent → Classification → Routing → Email Draft Creation
```

## Setup Instructions

### Prerequisites

- n8n instance (cloud or self-hosted)
- Google Workspace account with Sheets and Gmail access
- Anthropic API key for Claude AI model

### Required Credentials

1. **Google Sheets OAuth2**: For reading/writing to Google Sheets
2. **Gmail OAuth2**: For creating email drafts
3. **Anthropic API**: For AI-powered lead processing

### Google Sheets Structure

#### 1. Leads Database Sheet
```
| Id | name | email | company | role | message | priority | category | next_action | assigned_to |
```

#### 2. Team Routing Info Sheet
```
| category | owner_name | owner_email |
```

#### 3. Subject and Body Templates Sheet
```
| category | audience | subject_template | body_template | cc_default |
```

### Installation

1. **Import Workflow**
   ```bash
   # Import the workflow JSON file into your n8n instance
   ```

2. **Configure Credentials**
   - Set up Google Sheets OAuth2 credentials
   - Set up Gmail OAuth2 credentials
   - Add Anthropic API key

3. **Update Sheet IDs**
   - Replace the Google Sheet document ID with your actual sheet ID
   - Verify sheet names match your setup

4. **Test the Workflow**
   - Add a test lead to your Google Sheet
   - Monitor the workflow execution

## Lead Classification Logic

### Priority Levels
- **High**: Enterprise clients, security reviews, urgent requests with budget
- **Medium**: Mid-market prospects with concrete needs or referrals
- **Low**: Small companies with vague interest
- **Spam**: Crypto, affiliate marketing, promotional content

### Categories
- **Demo**: Demo, pilot, trial, or sandbox requests
- **Security**: SOC2, ISO, SSO, BAA, DPA compliance inquiries
- **Support**: Login, API, webhook, or billing issues
- **Pricing**: Pricing, tiers, or seat count questions
- **Sales**: General evaluation inquiries
- **Spam**: Promotional or irrelevant content

## Email Templates

### Internal Handoffs (Demo/Security)
- **To**: Assigned team member
- **Subject**: "New [category] lead – [company] – [name]"
- **Content**: Need summary, key context, proposed next steps

### Prospect Responses (Support/Pricing/Sales)
- **To**: Lead's email address
- **Subject**: "Re: [company] – next steps"
- **Content**: Acknowledgment, helpful information, clear call-to-action

## Customization

### Modifying Classification Rules

Edit the system prompt in the "Lead Triage Agent" node to adjust:
- Priority criteria
- Category definitions
- Routing logic
- Email template selection

### Adding New Categories

1. Update the system prompt with new category definitions
2. Add corresponding entries to the Team Routing Info sheet
3. Create email templates for the new category

### Extending Functionality

The workflow can be extended with additional tools:
- Calendar scheduling integration
- CRM system updates
- Slack notifications
- Custom webhook triggers

## Monitoring and Maintenance

### Key Metrics to Track
- Lead processing time
- Classification accuracy
- Email response rates
- Team workload distribution

### Regular Maintenance Tasks
- Review and update classification criteria
- Update email templates based on performance
- Monitor for new spam patterns
- Validate team routing assignments

## Security Considerations

- All API credentials are stored securely in n8n
- Email drafts are created but not automatically sent
- Lead data remains within your Google Workspace
- AI processing uses encrypted connections

## Troubleshooting

### Common Issues

1. **Workflow not triggering**
   - Verify Google Sheets trigger permissions
   - Check sheet ID and name configuration

2. **Classification errors**
   - Review system prompt for clarity
   - Check AI model configuration

3. **Email draft creation fails**
   - Verify Gmail OAuth2 permissions
   - Check email template formatting

## Contributing

To contribute improvements:
1. Test changes in a development environment
2. Document any new features or modifications
3. Ensure backward compatibility with existing data

## License

This workflow is provided as-is for educational and commercial use. Please ensure compliance with all service provider terms of use.

## Support

For support with this workflow:
- Check n8n community forums
- Review Google Workspace API documentation
- Consult Anthropic API documentation

---

**Note**: This is a sophisticated AI agent that requires proper setup and testing. Always start with a small dataset and gradually scale up after validating the classification accuracy and email generation quality.
