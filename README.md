Intelligent E-Commerce Sales Assistant with Memory and Product Catalog Integration

Overview

This n8n workflow creates an AI-powered sales chatbot that automatically extracts customer information, maintains conversation memory, retrieves product details from Google Sheets, and provides personalized responses using OpenAI GPT-4.

What This Workflow Does

The system receives chat messages, extracts customer details (name, email, phone, product interests) using JavaScript, stores information in Supabase, retrieves product data from Google Sheets, and generates personalized AI responses while maintaining conversation context across sessions.

Key Features

Automated Customer Data Extraction - Captures name, email, phone, and product interests from natural conversation
Conversation Memory - Maintains chat history across sessions using Supabase
Product Catalog Integration - Retrieves real-time product information from Google Sheets
Intent Detection - Identifies customer intent: buy, return, complaint, or support
Multi-Format Phone Support - Handles Pakistani phone formats (03XX, +92, 92)
Context-Aware Responses - Uses past conversation history for personalized answers

Business Use Cases

E-Commerce Customer Support - Automate product inquiries and sales conversations
Lead Generation - Capture customer contact details automatically
Product Recommendation - Suggest products based on interests and history
Order Management - Handle purchase inquiries with real product information
Sales Automation - Guide customers from discovery to purchase

Workflow Architecture

Chat Trigger - Receives messages via webhook and captures session ID
JavaScript Data Extraction - Parses messages using regex to extract customer data
Field Mapping - Prepares extracted data for AI agent and database
AI Agent - Processes queries, accesses tools, generates responses
OpenAI Chat Model - Powers AI with GPT-4 mini for natural conversations
Simple Memory Buffer - Maintains conversation history per session
Product Info Tool - Retrieves product details from Google Sheets
Store Memory Tool - Saves customer data and interactions to Supabase
Get Memory Tool - Retrieves past customer interactions for personalization

Prerequisites

Required Services

n8n instance (version 1.0 or higher)
OpenAI API account with GPT-4 access
Google account with Sheets API enabled
Supabase account with configured project

Required Credentials

OpenAI API Key
Google Sheets OAuth2 Credentials
Supabase Project URL and Service Key

Database Setup

Create Supabase table "Memory Storage" with these columns:

id - Auto-generated primary key
email - TEXT
name - TEXT
customer_phone - TEXT
session ID - TEXT
memory - TEXT
Customer_Interest - TEXT
created_at - TIMESTAMP

Google Sheets Setup

Create a sheet with these columns:

product_url - Link to product page
product Name - Name of product
product price - Product price
product Description - Detailed description
product Topic - Category or topic

Installation Steps

Import Workflow - Download JSON and import into n8n
Configure OpenAI - Add API key in OpenAI Chat Model node
Configure Google Sheets - Add OAuth2 credentials and select your product sheet
Configure Supabase - Add project URL and service key in both memory nodes
Test Webhook - Copy webhook URL and test with sample message

Customer Data Extraction Patterns

Email Detection - Matches standard email format (user@domain.com)
Phone Number - Supports 03XXXXXXXXX, +923XXXXXXXXX, 923XXXXXXXXX
Name Extraction - Detects "my name is", "I am", "I'm", "this is"
Product Interest - Identifies "buy", "looking for", "need", "want", "purchase"
Intent Classification - buy, return, complaint, support, or unknown

AI Agent Behavior

Uses current date/time for context
Retrieves past conversations before responding
Always checks Google Sheets for product questions
Stores customer insights after every message
Never reveals use of Google Sheets or Supabase
Guides customers toward product discovery and purchase

Customization Options

Modify Extraction Logic - Edit JavaScript code to change regex patterns
Adjust AI Personality - Update system message in AI Agent node
Add Product Columns - Extend Google Sheets and update tool configuration
Extend Memory Fields - Add columns to Supabase and update field mappings

Example Conversation Flow

User: "Hi, my name is Sarah and my email is sarah@example.com"
System: Extracts name and email, stores in Supabase
AI: "Hello Sarah! How can I help you today?"

User: "I'm looking for wireless earbuds"
System: Extracts product interest, retrieves past memory, searches Google Sheet
AI: Responds with product details and purchase link, stores interest

User: "What's the price?"
AI: Retrieves last product from memory, responds with exact price

Troubleshooting

Webhook Not Working - Verify URL is accessible and chat platform is configured
Data Not Extracting - Check regex patterns in JavaScript code
Google Sheets Failed - Confirm OAuth2 credentials and sheet permissions
Supabase Errors - Verify table name, field names, and data types match
Memory Not Storing - Check tool configuration and Supabase credentials
Phone Not Detected - Ensure format matches Pakistani patterns

Performance Optimization

Reduce API Costs - Implement caching for common queries, use shorter prompts
Improve Speed - Enable parallel tool execution, index Supabase tables
Scale for Volume - Implement rate limiting, use connection pooling

Security Best Practices

Store all API keys in n8n credential manager
Use environment variables for sensitive data
Implement proper access controls on Supabase
Rotate API keys regularly
Monitor API usage for anomalies

Integration Possibilities

CRM Systems - Export to Salesforce, HubSpot, or Zoho
Email Marketing - Sync with Mailchimp or SendGrid
Analytics - Connect to Metabase or Google Data Studio
Payment Gateways - Integrate Stripe or PayPal
Notifications - Send alerts via Slack or SMS

Future Enhancements

Voice integration with speech-to-text
Multilingual support (Urdu and English)
Sentiment analysis for customer satisfaction
Advanced product recommendations
Automated follow-up campaigns

Contributing

Fork this repository, create a feature branch, make changes, test thoroughly, and submit a pull request with detailed description.

License

MIT License - Free for personal and commercial use.

Support

For issues or questions, open an issue in this repository.

Built With

n8n workflow automation
OpenAI GPT-4 language model
Google Sheets for product catalog
Supabase for data storage
