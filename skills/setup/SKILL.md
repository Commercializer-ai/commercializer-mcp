---
name: setup
description: Connect Commercializer and check it works — sign in to commercializer.ai, choose the workspace, and confirm the tools answer. Use right after installing, or when the Commercializer tools are missing, ask to sign in, or answer 401.
---

Help the person connect Commercializer.

1. If the Commercializer tools are not available yet, the client has not signed in. Tell the person to start the
   sign-in their client offers for the `commercializer` server (in most clients a "Connect", "Sign in" or
   "Authenticate" button beside it; in Claude Code `/mcp`, in Codex `codex mcp login commercializer`). A page on
   commercializer.ai opens: they sign in, choose the workspace it reaches and press Allow.
2. With no account yet, they start one at https://commercializer.ai; every plan begins with a trial.
3. Once connected, call `get_profile` and greet them with their company's name and one line of what is kept about it.
   With no primary profile yet, call `list_profiles` and say they can set their company up on commercializer.ai.
4. If a tool answers that the workspace's plan does not run something, name the plan that does.

A client that cannot open a browser (a script, a CI job, the GitHub Copilot coding agent) uses an API key instead: made
on the MCP page of commercializer.ai, sent as `Authorization: Bearer <key>`. The full guide for each client is at
https://github.com/Commercializer-ai/commercializer/tree/main/docs.
