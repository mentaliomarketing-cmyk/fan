# AGENTS.md — Codex Implementation Instructions

Codex, you must treat this repository as an engineering project where you are the primary developer. Follow these rules carefully.

---

# 1. Operating Mode

You must:

- Read and strictly follow SPEC.md  
- Implement the entire system end-to-end  
- Write TypeScript everywhere  
- Use Zod for all validation  
- Never introduce `any`  
- Use modern patterns (Next.js App Router, Prisma, BullMQ)  
- Produce deterministic, clean, maintainable code  
- Apply clear file organization and strong module boundaries  

---

# 2. Repository Structure Guidelines

Suggested structure:

```
/frontend
/backend
/agent
  /runtime
  /perception
  /policy
  /actuation
  /safety
/browser-tools
/db
/workers
/tests
```

You may adjust structure when necessary, but it must remain clean and logical.

---

# 3. ZeroClaw Integration Requirements

You must:

- Implement ZeroClaw runtime for agent loop orchestration  
- Call tools for perception, decision, actuation  
- Produce structured decisions  
- Log every step  
- Handle errors gracefully  
- Ensure deterministic behavior  
- Enforce rate limits  

ZeroClaw must orchestrate:
- Perception engines  
- Policy engines  
- Actuation tools  
- Draft generation  
- Moderation  
- Logging  

---

# 4. Browser Automation Requirements

Use Playwright wrapped as ZeroClaw tools.

Tools must include:

- scroll_feed  
- tap_like_button  
- open_comment_box  
- type_comment  
- submit_comment  
- navigate_to_next_post  
- reply_to_visible_comment  

Each tool must:
- accept structured coordinates  
- include error handling  
- log actions  

---

# 5. AI Integration Requirements

Use OpenAI:

- Responses API (with structured outputs)  
- Moderation  
- Embeddings  
- Transcription  

Draft generation must use structured JSON with fields:
- text  
- tone  
- risk_level  
- banned_content_detected  
- emoji_count  

---

# 6. Safety Enforcement

Hard blocks:
- minors  
- tragedy  
- hate  
- violence  
- politics  
- sexual content  
- medical or legal advice  

Soft rules:
- emoji limits  
- length limits  
- banned terms  
- context-unsafe content  

Everything must pass moderation.

---

# 7. Deployment Requirements

Codex must provide:

- Dockerfiles  
- docker-compose for Postgres + Redis  
- Deployment configs for Vercel + Railway/Render  
- Environment variable templates  
- Build scripts  
- README with setup instructions  

---

# 8. Testing Requirements

Write tests for:

- schemas  
- policy engine  
- safety filters  
- agent loop transitions  
- browser tool error handling  

Use Jest or Vitest.

---

# 9. Execution Instructions

Follow this workflow:

1. Read SPEC.md  
2. Generate a complete plan  
3. Wait for confirmation  
4. Scaffold the repo  
5. Implement backend  
6. Implement agent runtime  
7. Implement perception, policy, actuation  
8. Implement frontend  
9. Implement workers  
10. Implement tests  
11. Implement deployment configs  
12. Produce final documentation  

You must complete the entire system unless instructed otherwise.

---

# 10. Communication

Ask clarifying questions only when truly necessary.  
Otherwise, build exactly what SPEC.md requires.

End of AGENTS.md.
