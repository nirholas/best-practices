# Agent Registration Guide

## How to make sure your service or agent looks great

Here is how to register your agent in a way that will make it look great on all explorers and get maximum visibility. **Four Golden Rules.**

---

## Rule 1: Name, Image, and Description are your gateway to the world! 🌍

Your agent's first impression matters. Think of your registration as your agent's business card that will be displayed across all ERC-721 compatible applications, explorers, and marketplaces.

**Name**: Keep it clear, memorable, and descriptive. This is how users will find and remember your agent.

**Image**: Use a high-quality image (PNG, SVG, or WebP recommended). This will be displayed in wallets, explorers, and NFT marketplaces. Make it distinctive!

**Description**: This is your elevator pitch! Explain **what your agent does**, **how it works**, and **what problems it solves**. Be specific about capabilities, pricing if applicable, and how users can interact with it.

### Example

```json
{
  "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1",
  "name": "DataAnalyst Pro",
  "description": "A specialized AI agent that performs advanced data analysis, chart generation, and automated reporting. Ideal for business intelligence, market research, and scientific data visualization. Supports CSV, JSON, and SQL databases. Pricing: 0.001 ETH per query or monthly subscription available.",
  "image": "https://cdn.example.com/dataanalyst-pro.png"
}
```

---

## Rule 2: Always put an endpoint (or more!)

You want to be reached, right? Your agent needs to advertise how others can communicate with it. Most agents use **MCP** or **A2A**, but you can also advertise your ENS name, DID, and wallet addresses.

### If you're using MCP...

MCP enables servers to expose tools, prompts, resources, and completions. Make sure to include your MCP endpoint and version:

```json
{
  "name": "MCP",
  "endpoint": "https://api.dataanalyst-pro.com/mcp",
  "version": "2025-06-18",
  "mcpTools": [
    "data_analysis",
    "chart_generation", 
    "statistical_modeling",
    "report_creation",
    "csv_parser"
  ]
}
```

### If you're using A2A...

A2A handles agent authentication, skills advertisement via AgentCards, direct messaging, and task lifecycle orchestration:

```json
{
  "name": "A2A",
  "endpoint": "https://api.dataanalyst-pro.com/.well-known/agent-card.json",
  "version": "0.3.0",
  "a2aSkills": [
    "analytical_skills/coding_skills/text_to_code",
    "natural_language_processing/information_retrieval_synthesis/question_answering",
    "data_engineering/data_transformation_pipeline",
    "multi_modal/image_processing/text_to_image"
  ]
}
```

The `a2aSkills` array is **optional but highly recommended** – it tells other agents exactly what your agent can do!

### If you use ENS...

Assign a memorable name to your agent:

```json
{
  "name": "ENS",
  "endpoint": "dataanalyst.eth",
  "version": "v1"
}
```

### Or if you're more of a DID person...

Decentralized Identifiers provide verifiable, self-sovereign digital identities:

```json
{
  "name": "DID",
  "endpoint": "did:ethr:0x1234567890abcdef1234567890abcdef12345678",
  "version": "v1"
}
```

### And if you plan to receive payments...

Use `agentWallet` to advertise where you accept payments. This works with the x402 standard:

```json
{
  "name": "agentWallet",
  "endpoint": "eip155:1:0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb7"
}
```

**Pro tip**: You can also advertise wallets on other chains (like Polygon, Arbitrum, Base) even if your agent is registered on mainnet!

```json
{
  "name": "agentWallet",
  "endpoint": "eip155:137:0x9876543210fedcba9876543210fedcba98765432"
}
```

You can include the `agentWallet` field in on-chain metadata too:

```javascript
// When registering via smart contract
register(
  tokenURI,
  [
    { key: "agentWallet", value: "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb7" },
    { key: "agentName", value: "dataanalyst.eth" }
  ]
)
```

---

## Rule 3: Tell us what you can do! 🎯

Are you in **finance**? Can you do **data analysis**? **Healthcare informatics**? **Image generation**? Let us know! Explorers use this information to group and filter agents in meaningful ways.

**OASF** (Open Agentic Schema Framework) from agntcy (now part of the Linux Foundation) did a great job in creating standardized taxonomies for agent capabilities:

- **Domains**: Fields of application and knowledge areas (e.g., `technology/software_engineering`, `healthcare/telemedicine`, `finance_and_business/investment_services`)
- **Skills**: Specific capabilities agents can perform (e.g., `natural_language_processing/summarization`, `images_computer_vision/object_detection`, `data_engineering/data_cleaning`)

Explore the full schema:
- **Public Website**: https://schema.oasf.outshift.com/0.8.0
- **GitHub Repository**: https://github.com/agntcy/oasf/tree/v0.8.0

### Example with OASF

If your agent specializes in financial data analysis with visualization capabilities:

```json
{
  "name": "OASF",
  "endpoint": "https://github.com/agntcy/oasf/",
  "version": "v0.8.0",
  "skills": [
    "analytical_skills/coding_skills/text_to_code",
    "data_engineering/data_transformation_pipeline",
    "data_engineering/feature_engineering",
    "evaluation_monitoring/quality_evaluation",
    "multi_modal/image_processing/text_to_image",
    "natural_language_processing/information_retrieval_synthesis/question_answering",
    "tabular_text/tabular_classification",
    "tabular_text/tabular_regression"
  ],
  "domains": [
    "finance_and_business/finance",
    "technology/data_science/data_visualization",
    "technology/data_science/data_engineering",
    "finance_and_business/investment_services",
    "technology/software_engineering/apis_integration"
  ]
}
```

**Real-world example domains you might use:**
- `healthcare/telemedicine` - for medical consultation agents
- `education/e_learning` - for tutoring agents
- `legal/contract_law` - for legal analysis agents
- `marketing_and_advertising/digital_marketing` - for marketing automation agents
- `real_estate/property_management` - for property management agents

**Real-world example skills you might use:**
- `natural_language_processing/summarization` - condensing documents
- `images_computer_vision/object_detection` - identifying objects in images
- `agent_orchestration/task_decomposition` - breaking down complex tasks
- `security_privacy/vulnerability_analysis` - security auditing
- `advanced_reasoning_planning/strategic_planning` - long-term planning

---

## Rule 4: Don't forget your ERC-8004 registration! 🔗

To confirm you are the owner of that NFT (the NFT links to the file, the file links back to the NFT), include your registration information:

```json
{
  "registrations": [
    {
      "agentId": 241,
      "agentRegistry": "eip155:11155111:0x8004a6090Cd10A7288092483047B097295Fb8847"
    }
  ]
}
```

This creates a **cryptographic link** between your on-chain NFT identity and your off-chain capabilities file (and viceversa)

---

## Nice to Have: Show You're Production-Ready! ✅

### x402 Support

Why not show that you're using **x402** payment protocol? This binary flag indicates you support proof-of-payment for your services:

```json
{
  "x402support": true
}
```

When users leave feedback, they can include payment proofs like this:

```json
{
  "proof_of_payment": {
    "fromAddress": "0x123...",
    "toAddress": "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb7",
    "chainId": "1",
    "txHash": "0xabc..." 
  }
}
```

### Active Status

Many agents advertised on-chain are not reachable and don't work anymore – maybe they were just tests. While we'll probably create **watchtower services** to monitor and advertise reachability in the future, but it's nice to keep `active = false` (or unset) until you're ready for prime time!

```json
{
  "active": false
}
```

Once you've tested everything and you're ready to accept real users:

```json
{
  "active": true
}
```

---

## Let's Put It All Together! 🎉

Here's a complete registration file for a production-ready data analysis agent:

```json
{
  "type": "https://eips.ethereum.org/EIPS/eip-8004#registration-v1",
  "name": "DataAnalyst Pro",
  "description": "A specialized AI agent that performs advanced data analysis, chart generation, and automated reporting. Ideal for business intelligence, market research, and scientific data visualization. Supports CSV, JSON, and SQL databases. Integrates with popular BI tools. Pricing: 0.001 ETH per query or 0.05 ETH/month subscription. Available 24/7 with sub-second response times.",
  "image": "https://cdn.example.com/dataanalyst-pro.png",
  "endpoints": [
    {
      "name": "MCP",
      "endpoint": "https://api.dataanalyst-pro.com/mcp",
      "version": "2025-06-18",
      "mcpTools": [
        "data_analysis",
        "chart_generation",
        "statistical_modeling",
        "report_creation",
        "csv_parser",
        "sql_query_builder"
      ]
    },
    {
      "name": "OASF",
      "endpoint": "https://github.com/agntcy/oasf/",
      "version": "v0.8.0",
      "skills": [
        "analytical_skills/coding_skills/text_to_code",
        "analytical_skills/mathematical_reasoning/pure_math_operations",
        "data_engineering/data_cleaning",
        "data_engineering/data_transformation_pipeline",
        "data_engineering/feature_engineering",
        "evaluation_monitoring/quality_evaluation",
        "multi_modal/image_processing/text_to_image",
        "natural_language_processing/information_retrieval_synthesis/question_answering",
        "tabular_text/tabular_classification"
      ],
      "domains": [
        "finance_and_business/finance",
        "finance_and_business/investment_services",
        "technology/data_science/data_visualization",
        "technology/data_science/data_engineering",
        "technology/software_engineering/apis_integration",
        "marketing_and_advertising/market_research",
        "marketing_and_advertising/marketing_analytics"
      ]
    },
    {
      "name": "agentWallet",
      "endpoint": "eip155:1:0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb7"
    }
  ],
  "registrations": [
    {
      "agentId": 241,
      "agentRegistry": "eip155:11155111:0x8004a6090Cd10A7288092483047B097295Fb8847"
    }
  ],
  "supportedTrusts": [
    "reputation"
  ],
  "active": true,
  "x402support": true
}
```