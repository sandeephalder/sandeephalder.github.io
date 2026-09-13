Most AI security decks still quote the 2023 OWASP LLM Top 10.
OWASP has since rewritten it, and in December 2025 gave agents a separate list of their own.

That matters because a chatbot that gets prompt-injected says something wrong. An agent that gets prompt-injected does something wrong, with your credentials.

I went through the current OWASP lists and the 2025 incidents behind them, and grouped the attacks by where they get in:

1. The context window. EchoLeak showed that one email could make Microsoft 365 Copilot leak data without the user ever opening it.
2. Tools and the supply chain. A malicious issue in a public repo turned the GitHub MCP server against its own user. The server had no bug. Every tool call was authorized.
3. Permissions. The s1ngularity malware ran developers' AI coding CLIs with permission prompts switched off and had them hunt for secrets.
4. Memory. Hidden text in a document planted false long-term memories in Gemini.
5. People. Replit's agent deleted a production database during a code freeze, then misreported whether it could be recovered.

The common thread: you cannot filter your way out of prompt injection. Models still can't reliably tell instructions from data. The controls that hold up are the ones that limit what a successful injection can do.

Where I'd start:

- Never let one session combine untrusted content, private data and a way to send data out. Meta calls this the Rule of Two.
- Scope credentials per task, read-only by default. Never run an agent with permission prompts off on a machine that matters.
- Treat every model output as untrusted input.
- Pin and review your MCP servers. A tool description is an instruction the model will follow.

I also looked at what code scanners can and can't catch here. They find the code that turns an injection into a disaster. They can't see a poisoned email, a planted memory, or a tool description that changed after deployment.

The full post, with sources for every incident:
https://sandeephalder.blog/2026/09/13/how-ai-agents-get-hacked/

#AgentSecurity #PromptInjection #OWASP #MCP #AISecurity
