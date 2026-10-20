🤖 WP AI Platform
Production WordPress AI Agent Framework
WP AI Platform is a production-oriented WordPress AI Agent framework designed to bring modern Generative AI capabilities directly into WordPress websites.
It provides an extensible architecture for AI chat, knowledge bases, RAG-ready workflows, tool calling, lead collection, WooCommerce integration, REST APIs, usage tracking, security controls, and AI provider abstraction.
🔗 Repository:
https://github.com/opspj007/WP-AI-Platform-Production-WordPress-AI-Agent-Framework
________________________________________
🚀 Features
🧠 AI Agent
•	AI-powered website assistant
•	Gemini integration
•	OpenAI integration
•	Provider abstraction
•	Custom system prompts
•	Conversation history
•	Extensible AI architecture
•	AI tool registry
•	Tool-calling foundation
•	Server-side API communication
📚 Knowledge Base & RAG Foundation
•	Knowledge source management
•	Website/content ingestion
•	Text chunking
•	Content hashing
•	Knowledge-source status tracking
•	Database-backed knowledge storage
•	RAG-ready retrieval architecture
The architecture is designed to be extended with:
•	Embeddings
•	Vector databases
•	Semantic search
•	Hybrid search
•	PDF/document ingestion
•	Website crawling
________________________________________
💬 AI Customer Support
The plugin provides a frontend AI chat interface that can be embedded into WordPress pages.
Example:
<div data-wpai-chat></div>
The frontend communicates with the WordPress REST API rather than exposing AI provider credentials in browser JavaScript.
________________________________________
🔌 REST API
The framework exposes versioned REST endpoints.
AI Chat
POST /wp-json/wp-ai/v1/chat
Example:
{
  "message": "What services does your company provide?"
}
Lead Collection
POST /wp-json/wp-ai/v1/leads
Example:
{
  "name": "John Doe",
  "email": "john@example.com",
  "phone": "+911234567890",
  "source": "ai-chat"
}
Knowledge Source
POST /wp-json/wp-ai/v1/knowledge
Example:
{
  "title": "Company FAQ",
  "content": "Our company provides web development and AI solutions."
}
Knowledge management endpoints require appropriate WordPress administrator capabilities.
________________________________________
🏗️ Architecture
┌──────────────────────────────────────────────┐
│              WordPress Website               │
├──────────────────────────────────────────────┤
│                AI Chat Widget                 │
└──────────────────────┬───────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────┐
│             WordPress REST API               │
│              /wp-ai/v1/*                     │
└──────────────────────┬───────────────────────┘
                       │
          ┌────────────┴────────────┐
          ▼                         ▼
┌──────────────────┐       ┌──────────────────┐
│   AI Agent       │       │  Lead Manager    │
└────────┬─────────┘       └──────────────────┘
         │
         ▼
┌──────────────────────────────────────────────┐
│             Provider Factory                 │
├──────────────────────┬───────────────────────┤
│                      │                       │
▼                      ▼                       │
Gemini               OpenAI                    │
│                      │                       │
└──────────────────────┴───────────────────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Knowledge Layer  │
              │ RAG Foundation   │
              └──────────────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Custom WP Tables │
              └──────────────────┘
________________________________________
📁 Project Structure
wp-ai-platform/
│
├── wp-ai-platform.php
├── uninstall.php
├── README.md
│
├── includes/
│   │
│   ├── Core/
│   │   ├── Activator.php
│   │   └── Deactivator.php
│   │
│   ├── Database/
│   │   └── Schema.php
│   │
│   ├── Security/
│   │   ├── RateLimiter.php
│   │   └── AuditLogger.php
│   │
│   ├── AI/
│   │   ├── AIProviderInterface.php
│   │   ├── GeminiProvider.php
│   │   ├── OpenAIProvider.php
│   │   ├── ProviderFactory.php
│   │   ├── Agent.php
│   │   └── ToolRegistry.php
│   │
│   ├── REST/
│   │   ├── ChatController.php
│   │   ├── LeadController.php
│   │   └── KnowledgeController.php
│   │
│   ├── Admin/
│   │   └── Dashboard.php
│   │
│   └── Integrations/
│       └── WooCommerce.php
│
├── assets/
│   ├── css/
│   │   ├── admin.css
│   │   └── chat.css
│   │
│   └── js/
│       └── chat.js
│
└── templates/
    └── chat-widget.php
________________________________________
🗄️ Database Architecture
The plugin uses dedicated database tables instead of storing application data entirely in wp_options.
Conversations
wpai_conversations
Stores AI conversation sessions and metadata.
Messages
wpai_messages
Stores individual user and assistant messages.
Leads
wpai_leads
Stores leads collected through the AI assistant.
Knowledge Sources
wpai_knowledge_sources
Stores imported knowledge.
Knowledge Chunks
wpai_knowledge_chunks
Stores chunked knowledge content ready for future semantic retrieval.
AI Usage
wpai_usage
Tracks:
•	Provider
•	Model
•	Endpoint
•	Request duration
•	Status
•	Token fields
Audit Logs
wpai_audit_logs
Provides an application-level audit trail.
________________________________________
🔐 Security
Security is treated as a core part of the architecture.
Implemented:
•	WordPress capability checks
•	Input sanitization
•	Output escaping
•	Prepared database operations through $wpdb
•	REST permission callbacks
•	Rate limiting
•	Server-side API keys
•	API response validation
•	Audit logging
•	Controlled knowledge-management access
•	Secure uninstall process
API Keys
AI API keys are stored server-side in WordPress settings.
They are not placed inside frontend JavaScript.
Browser
   │
   │ Request
   ▼
WordPress REST API
   │
   ▼
AI Provider
This prevents exposing provider credentials directly to visitors.
________________________________________
⚡ Performance
The architecture is designed with WordPress production environments in mind.
Current foundation includes:
•	Database indexes
•	Transient-based rate limiting
•	Limited conversation history
•	Server-side API requests
•	Lightweight frontend widget
•	Dedicated database tables
Future production enhancements can include:
•	Persistent object caching
•	Redis
•	Async background processing
•	Queue workers
•	Response caching
•	Vector search caching
•	Batch embedding generation
________________________________________
🛒 WooCommerce Integration
When WooCommerce is active, the plugin registers an AI tool for product information.
The tool can retrieve:
Product ID
Product Name
Price
Stock Status
Product URL
This architecture can be extended into an AI commerce agent capable of:
•	Product search
•	Product recommendations
•	Order lookup
•	Order status
•	Customer support
•	Cart assistance
•	Product comparison
________________________________________
🧩 Tool Registry
The framework contains an extensible tool registry.
Example:
WPAI_Tool_Registry::register(
    'get_product',
    function ($args) {
        // Execute tool
    }
);
This allows developers to add custom AI tools without modifying the core agent architecture.
Potential tools:
search_products
get_order
create_lead
search_knowledge
get_company_info
book_appointment
check_inventory
send_email
________________________________________
🤖 AI Provider Abstraction
The plugin does not tightly couple the agent to a single AI provider.
Provider interface:
interface WPAI_AI_Provider_Interface {

    public function chat(
        array $messages,
        array $options = []
    );
}
Current providers:
Gemini
OpenAI
This makes the architecture easier to extend with additional providers.
Possible future providers:
Anthropic
Azure OpenAI
Google Vertex AI
OpenRouter
Local LLMs
Custom AI APIs
________________________________________
📊 Admin Dashboard
The WordPress admin dashboard provides an overview of:
•	AI requests
•	Leads
•	Knowledge sources
•	AI provider
•	Model configuration
•	System prompt
•	Rate limits
The dashboard is designed as the foundation for a larger AI operations console.
________________________________________
🛠️ Installation
1. Download
Download or clone the repository:
git clone https://github.com/opspj007/WP-AI-Platform-Production-WordPress-AI-Agent-Framework.git
2. Install
Copy the plugin into:
wp-content/plugins/wp-ai-platform/
Or create a ZIP:
zip -r wp-ai-platform.zip wp-ai-platform/
3. Activate
From:
WordPress
→ Plugins
→ WP AI Platform
→ Activate
4. Configure
Open:
WordPress Admin
→ WP AI Platform
Configure:
AI Provider
API Key
Model
System Prompt
Rate Limit
________________________________________
💻 Requirements
WordPress 6.0+
PHP 7.4+
MySQL 5.7+
MariaDB 10.4+
Optional:
WooCommerce
________________________________________
🧪 Example AI Workflow
Visitor
   │
   ▼
AI Chat Widget
   │
   ▼
REST API
   │
   ▼
Rate Limiter
   │
   ▼
AI Agent
   │
   ├── Knowledge Search
   │
   ├── Tool Calling
   │
   ├── Lead Detection
   │
   └── AI Provider
   │
   ▼
Gemini / OpenAI
   │
   ▼
AI Response
   │
   ▼
Visitor
________________________________________
🚧 Production Roadmap
The current repository provides the core architecture. Planned improvements include:
Phase 1 — AI Infrastructure
•	Streaming responses
•	Structured outputs
•	Function calling
•	Advanced tool execution
•	Conversation persistence
•	Context management
Phase 2 — RAG
•	PDF ingestion
•	DOCX ingestion
•	Website crawler
•	Embeddings
•	Vector database
•	Semantic search
•	Hybrid retrieval
•	RAG citations
Phase 3 — AI Agents
•	Multi-step agents
•	Agent memory
•	Planning
•	Tool permissions
•	Human handoff
•	Approval workflows
Phase 4 — WordPress
•	Gutenberg integration
•	Elementor integration
•	WooCommerce order tools
•	WordPress content generation
•	SEO assistant
•	Media library AI
•	Automated content workflows
Phase 5 — Enterprise
•	Multi-site support
•	Multi-tenant architecture
•	User quotas
•	Usage-based billing
•	Team management
•	Advanced analytics
•	SSO
•	Audit compliance
•	Observability
________________________________________
🧑‍💻 Developer
Om Prakash Chaudhary
Senior Software Developer | WordPress Engineer | Generative AI Engineer
Areas of focus:
PHP
WordPress
Laravel
JavaScript
React
REST APIs
MySQL
Generative AI
AI Agents
RAG
Multimodal AI
Cloud & DevOps
AI-assisted Development
GitHub:
https://github.com/opspj007
________________________________________
📄 License
This project is released under the GPL-2.0-or-later license, consistent with WordPress plugin development.
________________________________________
⭐ Why This Project?
WP AI Platform demonstrates how WordPress can be extended from a traditional CMS into a modern AI application platform.
It combines:
WordPress Engineering + PHP Architecture + REST APIs + AI Agents + RAG + Tool Calling + WooCommerce + Security + Database Engineering
making it suitable as a foundation for building production AI-powered WordPress products.

