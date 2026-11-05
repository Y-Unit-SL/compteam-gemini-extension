---
trigger: model_decision
description: Use when the user asks about Compteam, BJJ or martial arts clubs, class schedules, membership plans, their own or a linked child's classes, attendance, or free trial inquiries.
---

# Compteam

Use the `compteam` MCP tools for Brazilian jiu-jitsu and martial arts club discovery, public class schedules, membership plans, and the signed-in member's classes, account status, and attendance. Follow the `compteam-training` skill for the full workflow.

- Public club, class, and price lookups work without signing in.
- Personal tools need Compteam OAuth. If a call reports that sign-in is required, ask the user to sign in to the Compteam MCP server (Gemini CLI: `/mcp auth compteam`; Antigravity: authenticate the server when prompted) and complete the browser sign-in.
- Confirm with the user before changing attendance or sending a trial inquiry.
- Never ask for passwords, OAuth codes, payment details, or identity documents.
