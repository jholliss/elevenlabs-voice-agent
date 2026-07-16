# Project: "Talk to James" — ElevenLabs Agent Demo

**Goal:** A personal ElevenLabs Conversational AI agent + webpage, built to
demo for an ElevenLabs Solutions Engineer application. The agent talks
about James Holliss's background; the page is styled to match ElevenLabs'
own dark, minimal aesthetic.

**Live agent ID:** `agent_01jz0scy5mfstt0azd5vtsy4gg`
(create/manage at https://elevenlabs.io/app/agents)

---

## What's done

### 1. Agent configuration
Drafted and handed over as `james-holliss-agent-config.md`:
- System prompt (persona, tone, what to cover, how to handle "why hire James")
- First message
- Knowledge base doc (expanded project notes beyond the CV bullet points)
- Voice recommendation: clone James's own voice rather than a stock voice
- Stretch idea: give the agent a real tool call (e.g. calendar booking)
  since MCP-based tool orchestration is James's actual specialty at
  SnapLogic — this would be the highest-leverage addition.

Source material: `JamesHollissCV.pdf` (uploaded by user) — 10+ years
consulting/engineering, currently Solutions Engineer at SnapLogic, built
their internal 40+ system MCP-based agent platform (37x LLM ROI), led
KYC/AML automation for a UK bank (5x throughput), ran Civica's AI in
Government GTM (£6m revenue), MSc CS from UCL, background in audio
engineering (BBC/ITV/C4/Sky) before retraining into tech.

**Status:** drafted, not yet pasted into the ElevenLabs dashboard by the
user. Not yet tested end-to-end in the ElevenLabs UI.

### 2. Webpage
Built as a static site (no framework, no backend) at:
```
talk-to-james/index.html
```
- Single HTML file, dark theme matching ElevenLabs' visual language
  (near-black background, restrained type, centered layout).
- Embeds the official widget via:
  ```html
  <elevenlabs-convai
    agent-id="agent_01jz0scy5mfstt0azd5vtsy4gg"
    variant="expanded"
    action-text="Talk to James's AI agent"
    start-call-text="Start conversation"
    end-call-text="End conversation"
  ></elevenlabs-convai>
  <script src="https://unpkg.com/@elevenlabs/convai-widget-embed" async type="text/javascript"></script>
  ```
- Chose plain HTML over Streamlit deliberately: the widget needs direct
  mic access (`getUserMedia`), and Streamlit's iframe sandboxing
  (`components.html`) adds friction with no upside here.

**Tested locally via:** `python3 -m http.server 8000` → `localhost:8000`

**Still to confirm on the ElevenLabs dashboard:**
- [ ] Agent authentication disabled (Advanced tab) — required for basic
      widget embed without a signed-URL backend.
- [ ] `localhost` and eventual production domain added to the agent's
      **Allowlist** (Security tab).

---

## Next steps / open items

1. **Paste the drafted system prompt, first message, and knowledge base**
   into the ElevenLabs dashboard for `agent_01jz0scy5mfstt0azd5vtsy4gg`,
   then test conversations (try "why should we hire James over another
   candidate" and "walk me through the SnapLogic platform").
2. **Voice cloning** — record a few clean samples and clone James's voice
   in ElevenLabs, then set it as the agent's voice.
3. **Optional stretch: real tool call.** Wire a calendar-booking action
   (e.g. via Cal.com integration or a small MCP server/webhook) so the
   agent can actually book a follow-up call during the conversation — a
   direct demonstration of the MCP orchestration work James already does
   professionally.
4. **Deploy beyond localhost.** Static host recommended (Vercel, Netlify,
   or GitHub Pages) — drag-and-drop the `talk-to-james/` folder, no
   server code required. Remember to add the live domain to the agent's
   Allowlist once deployed.
5. **Polish pass on the page** — confirm copy/tags, consider adding a
   short "about this demo" line noting it's a personal project (not an
   official ElevenLabs page), and check mobile responsiveness.

---

## Files referenced in this project
- `JamesHollissCV.pdf` — source CV (uploaded)
- `james-holliss-agent-config.md` — system prompt / first message /
  knowledge base draft for the ElevenLabs dashboard
- `talk-to-james/index.html` — the standalone webpage hosting the widget
