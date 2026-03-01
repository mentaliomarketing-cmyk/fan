# AI Instagram Community Manager + Autonomous Agent Spec (ZeroClaw-Powered)

This document defines the complete system for a fully autonomous Instagram Engagement Agent. Automate browsing, liking, commenting, replying, and UI interaction. Codex must implement the full system end-to-end.

---

# 1. Product Overview

The AI Instagram Agent is a ZeroClaw-powered autonomous system that:

- Browses the Instagram feed  
- Understands images, captions, comments  
- Decides to like, comment, skip, or reply  
- Generates high-quality, safe, on-brand comments  
- Replies to comments on the user’s own posts  
- Enforces rate limits & safety policies  
- Operates continuously  
- Logs all actions  
- Runs inside a browser automation environment  

The system must behave as a safe, brand-consistent autonomous agent.

---

# 2. Core Features

## Autonomous Feed Interaction
- Scroll feed  
- Detect posts  
- Capture screenshots  
- Identify UI elements (like button, comment box)  
- Understand content & context  
- Decide: skip / like / comment  

## Autonomous Commenting
- Generate short on-brand comments  
- Avoid repetitive phrases  
- Customize by context & history  

## Autonomous Replies
- Ingest comments on user's own posts  
- Generate replies  
- Auto-post low-risk replies  
- Route sensitive replies for human review  

## Brand Personality System
- Tone controls  
- Emoji rules  
- Formality & humor sliders  
- Banned phrases  
- Allowed CTAs  
- Style examples  

## Safety
- Disallow harmful topics  
- Block minors, tragedy, politics, NSFW  
- OpenAI moderation  
- Internal risk scoring  

## Rate Governance
- Hourly caps  
- Daily caps  
- Burst prevention  
- Quiet hours  
- Backoff on UI errors  

---

# 3. High-Level Architecture

```
Frontend (Next.js)
Backend API (Node.js)
Background Workers (BullMQ)
ZeroClaw Agent Runtime
Browser Automation Layer (Playwright)
AI Services (OpenAI)
Database (Postgres + Prisma)
Redis (Queues + State)
```

---

# 4. ZeroClaw Runtime

ZeroClaw acts as the “brain” of the agent:

### Task Loop
1. Observe (screenshot + DOM)  
2. Perceive (vision analysis)  
3. Decide (policy engine)  
4. Act (browser automation)  
5. Log  
6. Repeat  

### Required Behaviors
- Deterministic logic  
- Structured decisions  
- Full audit log  
- Robust error recovery  
- Rate limit compliance  

---

# 5. Perception Layer

ZeroClaw must orchestrate the following tools:

- `capture_screenshot()`  
- `extract_dom()`  
- `vision_analyze(screenshot)`  
- `parse_caption(dom)`  
- `ocr_text(screenshot)`  
- `classify_topics()`  
- `detect_sentiment()`  

Output structured context:

```json
{
  "poster": "username",
  "caption": "Beautiful day 🌸",
  "media_topics": ["nature", "travel"],
  "sentiment": "positive",
  "risk": "LOW",
  "visible_comments": [],
  "ui_locations": {
    "like_button": [...],
    "comment_box": [...],
    "post_area": [...]
  }
}
```

---

# 6. Policy Engine

Implements all decision logic:

### Engagement Rules
- When to like, comment, reply, or skip  
- Based on image category  
- Based on relationship with poster  

### Personality Rules
- Tone (warm, witty, minimal)  
- Humor level  
- Emoji usage  
- Banned terms  
- Max words  

### Safety & Risk
- Sensitive content blocks  
- Moderation filters  
- Risk scoring (LOW / MED / HIGH)  

### Rate Limits
- Hourly & daily caps  
- Quiet hours  
- Burst prevention  

Policy output schema:

```json
{
  "recommended_action": "COMMENT",
  "risk_level": "LOW",
  "tone": "warm",
  "requires_review": false
}
```

---

# 7. Draft Generation

Using OpenAI:

- Generate 1–3 candidate comments  
- Follow tone constraints  
- Enforce length & emoji rules  
- Remove banned phrases  
- Reject unsafe drafts  
- Choose best candidate  
- Provide fallback  

Uses structured outputs.

---

# 8. Actuation Layer (Browser Automation)

Must expose tools for ZeroClaw:

- `scroll_feed()`  
- `tap_like_button(location)`  
- `open_comment_box(location)`  
- `type_comment(text)`  
- `submit_comment()`  
- `navigate_to_next_post()`  
- `reply_to_visible_comment(text)`  

All actions must be deterministic, logged, and rate-limited.

---

# 9. Autonomous Agent Loop

1. `scroll_feed()`  
2. `capture_screenshot()`  
3. Perception → context  
4. Policy → decision  
5. If COMMENT:  
   - generate  
   - filter  
   - actuation  
6. Log action  
7. Next post  

All loops must respect safety & rate limits.

---

# 10. Data Models (Prisma)

Models include:

- User  
- InstagramConnection  
- BrandProfile  
- Media  
- Comment  
- ReplyDraft  
- ReplyPost  
- KnowledgeDoc  
- AgentActionLog  
- RateLimitState  

---

# 11. Backend API Endpoints

Implement:

- Auth  
- Instagram OAuth  
- Webhooks (comment events)  
- Comment ingestion  
- Draft regeneration  
- Posting replies  
- Agent control (pause/resume)  
- Settings update  
- Logs retrieval  

All must include Zod validation.

---

# 12. Frontend (Next.js)

Pages:

- Dashboard  
- Agent Activity Log  
- Comment Inbox  
- Draft Editor  
- Personality Settings  
- Safety Settings  
- OAuth Onboarding  

---

# 13. Workers (BullMQ)

Jobs:

- `agent:loop`  
- `ai:generate-draft`  
- `ai:enrich-media`  
- `policy:evaluate`  
- `post:reply`  

---

# 14. Safety & Moderation

Use OpenAI moderation + internal rules to block:

- Violence  
- Minors  
- Politics  
- Sexual content  
- Medical advice  
- Personal data  
- Crisis content  

---

# 15. Deployment Requirements

Codex must provide:

- Dockerfiles  
- docker-compose.yml (Postgres + Redis)  
- Railway/Render backend service  
- Vercel frontend  
- CI/CD pipeline  
- .env template  
- Production build scripts  

---

# 16. Testing

Tests required for:

- Zod schemas  
- Policy engine logic  
- Safety rules  
- Draft generation  
- Agent loop transitions  
- Browser action error handling  

---

# 17. Deliverables

Codex must produce:

- Complete repo  
- Full backend  
- Full frontend  
- Agent runtime  
- Browser tools  
- Workers  
- Database layer  
- Deployment configs  
- Logs + monitoring  
- Tests  
- Developer documentation

Implementation must strictly follow this spec.
