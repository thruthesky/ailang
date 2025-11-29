# AI Lang (Artificial Intelligence Language)

A high-dimensional meta-language system designed to deliver human intent to AI systems with maximum precision.

## What is AI Lang?

AI Lang is a sophisticated communication language system that goes beyond traditional natural language-based prompt engineering. It enables humans to interact with AI by understanding and utilizing the AI system's internal structure, knowledge access methods, agent collaboration patterns, and context management approaches.

**If a prompt is a sentence, AI Lang is more like a 'grammar'.**

## Why AI Lang?

When humans write prompts in natural language, intermediate tools (chatbots, agents, etc.) mix many elements before delivering to AI:
- System Prompts
- Context (Memory, Session Information)
- RAG (Retrieval-Augmented Generation)
- Agent Chains (Agent, MCP, etc.)
- Tool Usage Instructions
- And more...

Humans cannot communicate directly with AI. AI Lang provides a structured way to communicate more precisely with AI through these intermediaries.

## Key Features

- **AI-Friendly Structuring**: Expresses commands, constraints, intent, context, and roles more explicitly than natural language
- **System Layer Awareness**: Unifies RAG, tool calls, and multi-agent logic into a single grammar
- **Extensible Meta-Language**: Flexible structure based on sub-rules that can be applied even when models change
- **Intent-to-Action Loss Minimization**: Reduces ambiguity and compresses meaning into a form that AI can execute precisely

## Grammar (YAML-based)

AI Lang uses YAML format to convey intent to AI in a structured way:

```yaml
intent: CREATE. Add a chat feature.

persona:
  role: Python Backend Developer
  expertise: FastAPI, Authentication Systems

context:
  domain: Software Development
  language: Python
  framework: FastAPI

constraints:
  must:
    - Type safety guaranteed
    - Async processing support
  should:
    - Detailed documentation

output:
  type: code
  format: Python

request: |
  Implement a JWT token-based user
  authentication API.
```

## Intent Types

| Type | Description | Example |
|------|-------------|---------|
| CREATE | Generate something new | `intent: CREATE. Add a chat feature.` |
| UPDATE | Improve existing content | `intent: UPDATE. Improve the login screen.` |
| TRANSFORM | Transform content | `intent: TRANSFORM. Translate to Korean.` |
| ANALYZE | Analyze and evaluate | `intent: ANALYZE. Analyze performance issues.` |
| EXPLAIN | Explain and educate | `intent: EXPLAIN. Explain the auth system.` |
| VALIDATE | Verify and validate | `intent: VALIDATE. Verify API response.` |
| DEBUG | Fix bugs | `intent: DEBUG. Fix the login bug.` |
| TROUBLESHOOT | Resolve issues | `intent: TROUBLESHOOT. Resolve connection error.` |
| MIGRATE | Migration tasks | `intent: MIGRATE. Migrate to PostgreSQL.` |
| DECIDE | Decision support | `intent: DECIDE. React vs Vue?` |

## Website

Visit [ailang.dev](https://ailang.dev) for full documentation, examples, and specification.

## Community

- **GitHub**: [https://github.com/thruthesky/ailang](https://github.com/thruthesky/ailang)
- **Discussions**: [https://github.com/thruthesky/ailang/discussions](https://github.com/thruthesky/ailang/discussions)

## Contact

JaeHo Song <thruthesky@gmail.com>

## License

MIT License

© 2024 AI Lang Project
