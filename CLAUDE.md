# WhatsApp Helper - Digital Twin Research

> **IMPORTANT:** Every agent MUST read this file before starting work. Every agent MUST update this file after completing work.

---

## Project Overview

**Research Goal:** Explore whether LLMs can create a convincing digital facsimile of a person - specifically, can an AI replicate:
- Writing style and typing patterns
- Decision-making processes
- Emotional responses and reactions
- Memory and knowledge architecture

**What this is NOT:**
- Not for deception or tricking people
- Not for catfishing or impersonation without disclosure
- Not a production bot (research phase only)

**Use Case:** Personal research to see if AI can arrive at the same conclusions and replicate the thinking patterns of the user.

---

## Architecture (Current Phase)

```
Local Research Setup:
Your Phone ←→ WhatsApp ←→ WhatsApp MCP Bridge (Go) ←→ Claude Desktop
                                              ↓
                                        WhatsApp MCP Server (Python)
                                              ↓
                                          Behavior Layer (this research)
```

**Future phases may include:**
- VPS hosting for 24/7 operation
- Remote trigger mechanism (Telegram, web)
- Integration with Clawdbot or custom bot framework

---

## Tech Stack

### Current
- **Python 3.14.2** - Behavior layer and experiments
- **WhatsApp MCP** (lharries/whatsapp-mcp) - Bridge to WhatsApp Web API
- **Go** - Required for WhatsApp bridge
- **Claude Desktop** - LLM interaction layer
- **UV** - Python package manager
- **SQLite** - Local message storage

### Under Consideration
- **Clawdbot** - For 24/7 operation and remote triggering
- **whatsapp-python** - Alternative to MCP (needs research)
- **Vector DB** - For memory architecture experiments
- **MemGPT-style** - Hierarchical memory management

---

## Project Structure

```
whatsapp_helper/
├── .beads/              # Issue tracking (beads-sync branch)
├── .venv/               # Python virtual environment
├── .claude/             # Claude Code settings
├── research/            # Research notes and findings
│   ├── memory/          # Memory architecture experiments
│   ├── behavior/        # Behavioral replication studies
│   ├── style/           # Writing/style analysis
│   └── prompts/         # System prompts and templates
├── experiments/         # Individual experiment scripts
├── data/                # Test data (samples, not real conversations)
└── CLAUDE.md           # This file
```

---

## Research Questions

### Primary Questions

1. **Style Replication**
   - Can an LLM match typing patterns, slang, emoji use?
   - Can it replicate sentence structure and capitalization?
   - How many examples are needed before style is convincing?

2. **Decision Modeling**
   - Given the same context, does the AI make the same choice as the human?
   - Can "how would I react to X" examples train decision patterns?
   - What breaks the illusion? Where does it fail?

3. **Memory Architecture**
   - How do we give the AI "memories" it can reference?
   - What's important to remember vs. forget?
   - Can we implement selective memory (remember important, forget trivial)?
   - How does memory decay work?

4. **Authenticity Limits**
   - Where does the simulation break down?
   - What emotional cues does it miss?
   - Can it maintain consistency over long conversations?

### Secondary Questions

- How does context window size affect memory?
- Can RAG + vector stores improve memory?
- What's the role of "reflection" (Metacognitive processes)?
- How do we measure "success" - subjective or objective?

---

## Development Environment

### Python Virtual Environment
**Location:** `.venv/`
**Activation:** `source .venv/bin/activate` (automatic via direnv)

### Dependencies
```bash
# Python packages (add as needed)
pip install anthropic  # Claude API
pip install openai     # For comparison testing
pip install chromadb    # Vector store for memory experiments
pip install numpy      # Data analysis

# WhatsApp MCP setup (see docs/)
cd whatsapp-mcp/whatsapp-bridge
go run main.go  # First time: scan QR code

cd whatsapp-mcp/whatsapp-mcp-server
uv run main.py  # Start MCP server
```

### Environment Variables
```bash
# Required
ANTHROPIC_API_KEY=sk-ant-xxx  # Claude API key

# Optional for experiments
OPENAI_API_KEY=sk-xxx         # For comparison
WHATSAPP_PHONE=+1234567890    # Your number for testing
```

---

## Research Approach

### Phase 1: Data Collection
- Collect writing samples (messages, emails, notes)
- Analyze personal communication patterns
- Document decision-making examples
- Create "how I would react to X" scenarios

### Phase 2: Baseline Testing
- Test Claude with no personalization
- Measure differences in style, decisions, responses
- Establish control metrics

### Phase 3: Prompt Engineering
- Create system prompt with persona
- Inject knowledge and memories
- Add style guidelines
- Test against baseline

### Phase 4: Memory Architecture
- Implement basic memory (facts in prompt)
- Test hierarchical memory (MemGPT-style)
- Experiment with vector stores + RAG
- Test importance scoring and decay

### Phase 5: Evaluation
- Self-evaluation (does this feel like me?)
- Blind testing (can you tell which is real?)
- Long-form conversations (consistency over time)
- Edge cases (how does it handle unfamiliar situations?)

---

## Key Dependencies

### WhatsApp MCP
**Repo:** https://github.com/lharries/whatsapp-mcp
**Features:**
- Read/send WhatsApp messages via personal account
- Search contacts and messages
- Download media
- SQLite storage

**Security Note:** This MCP has full read/write access. No read-only mode exists.
**Mitigation:** Monitor outputs carefully. Research only, not production.

---

## Agent Instructions

### When Starting Work
1. Read this entire file (CLAUDE.md)
2. Activate venv: `source .venv/bin/activate`
3. Find work: Run `bd ready` to see available tasks
4. Claim task: `bd update <id> --status=in_progress`
5. Read the full issue: `bd show <id>`

### While Working
1. **Add progress comments** regularly (every 30-60 min of work)
2. **Document findings** in `research/` directory
3. **Test hypotheses** before drawing conclusions
4. **Be skeptical** - question whether behavior is convincing

### Comment Format:
```
PROGRESS: What I'm working on now
FINDINGS: Initial observations or results
NEXT: What I plan to do next
QUESTIONS: Things I'm unsure about
```

### When Finishing Work
1. **Document results** in research/ directory
2. **Run tests** if applicable
3. **Add completion comment:**
   ```
   DONE: What was completed
   FINDINGS: Research results
   NEXT_STEPS: Follow-up work needed
   ```
4. **Update issue:** `bd update <id> --status=pending_review`
5. **DO NOT close issues** - human will review

---

## Available MCP Tools

### zai-mcp-server
- Image/video analysis
- Error screenshot diagnosis
- UI to code conversion
- Technical diagram understanding
- Text extraction (OCR)
- Data visualization analysis
- Video content analysis

### Beads
- `bd` commands for issue tracking
- `bd sync` to push to remote

---

## Git Permissions

**GitHub Access:**
- **Username:** MoonMayne
- **Protocol:** HTTPS (not SSH)
- **URL format:** https://github.com/MoonMayne/whatsapp_helper.git

**Allowed:**
- ✅ git commit
- ✅ git push
- ✅ git pull
- ✅ git branch
- ✅ git status, log, diff, show

**Blocked (destructive):**
- ❌ rm, rmdir, rm -rf
- ❌ git reset --hard
- ❌ git push --force
- ❌ git branch -D
- ❌ git checkout --orphan
- ❌ git clean -fd*

**All permissions controlled via** `.claude/settings.json`

---

## Coding Conventions

1. **Python:** Use type hints, docstrings for functions
2. **Research:** Document assumptions, methodology, results
3. **Experiments:** Keep control groups, test one variable at a time
4. **Documentation:** README.md for each experiment
5. **Validation:** Run `python -m pytest` if tests exist

---

## Safety and Ethics

**IMPORTANT:** This research must not:
- Deceive people into thinking they're talking to the real you
- Impersonate you for fraud or manipulation
- Catfish or trick people

**Acceptable Use:**
- Research testing (you review all outputs)
- Personal curiosity about AI capabilities
- Open discussion about AI nature with participants
- Academic/educational purposes

**If deploying:**
- Clear disclosure that it's an AI
- Opt-in consent from conversation partners
- Ability for human to override or intervene

---

## Known Limitations

### LLM Memory (Current State)
- Flat context window (no selective memory)
- No learning from experience
- Can't distinguish important vs trivial information
- No emotional weighting of memories
- Static (no reconsolidation on recall)

### What Makes Human Memory Different
- Associative (linked by meaning, not just tokens)
- Decay over time (forget things naturally)
- Reconsolidation (memories change when recalled)
- Emotional salience (remember what matters)
- Hierarchical (working memory → short-term → long-term)

### Research Trying to Bridge Gap (2025-2026)
- **HiMem** (Jan 2026) - Hierarchical long-term memory for long-horizon dialogues; links episodic events with abstract knowledge
- **Agentic Reasoning for LLMs** (Jan 2026) - Self-reflection, memory mechanisms, multi-agent coordination
- **Human-Like Remembering and Forgetting** (2025) - Integrates ACT-R cognitive architecture for human-like memory decay
- **DAM-LLM** (Oct 2025) - Dynamic affective memory; emotional weighting of memories
- **"A Survey on the Evolution of LLM Agent Memory"** (Jan 2026) - Overview of memory mechanism progression
- **MemGPT** (2024-2025) - OS-inspired hierarchical memory management (RAM vs disk analogy)
- **Persistent Memory Frameworks** (2025) - Long-term retention, selective retrieval, dynamic organization

---

## Related Research

### Academic Papers (2025-2026)
- "HiMem: Hierarchical Long-Term Memory for LLM Long-Horizon Agents" (arXiv, Jan 2026)
- "Agentic Reasoning for Large Language Models" (ResearchGate, Jan 2026)
- "Human-Like Remembering and Forgetting in LLM Agents" (ACM, 2025) - ACT-R integration
- "Dynamic Affective Memory Management for Personalized Dialogue" (arXiv, Oct 2025)
- "A Survey on the Evolution of LLM Agent Memory" (Preprints, Jan 2026)

### Earlier Foundational Work
- "Generative Agents: Interactive Simulacra of Human Behavior" (Stanford, 2023)
- "MemGPT: Towards LLMs as Operating Systems" (UC Berkeley, 2024)

### Industry
- **Character.AI** - Personality-focused chatbots
- **xAI "Human Emulators"** - Bots in org charts
- **Microsoft "AI Workers"** - Delegation to AI agents
- **Replika** - Personal AI companions

### Fiction/Media
- *Black Mirror* "Be Right Back" - AI recreation of deceased partner
- *Ex Machina* - Hyper-realistic AI
- *Star Trek* (Data) - Android learning humanity
- *Westworld* - Memory and consciousness in AI

---

## Next Steps

**Immediate:**
1. Set up WhatsApp MCP locally
2. Collect baseline writing samples
3. Create initial persona prompt
4. Run first experiments

**Short-term:**
1. Test style replication accuracy
2. Implement basic memory system
3. Compare Claude vs other LLMs
4. Document where illusion breaks

**Long-term:**
1. Explore memory architecture options
2. Test continuous conversation consistency
3. Measure "authenticity" metrics
4. Consider remote deployment options
