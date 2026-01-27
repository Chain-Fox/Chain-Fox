# Chain-Fox Roadmap

> Focus: move from code-only checks to realistic Web3 risk analysis using skill-based workflows.

---

## Goals

* Replace one-shot LLM audits with **step-by-step Skills**
* Make existing code checkers **agentic and skill-aware**
* Detect **real attack risks** (rug pulls, malicious websites), not just code smells
* Output **explainable risk signals**, not binary results
* Reduce false negatives and false positives using real-world cases
* Stay driven by real usage, feedback, and interaction

---

## Month 1: Core Capability Shift

### Rug Pull Risk Detection (v0)

* [ ] Detect risky contract permissions

  * [ ] mint / burn
  * [ ] ownership & upgradeability
  * [ ] liquidity control
* [ ] Analyze on-chain behavior

  * [ ] liquidity add/remove patterns
  * [ ] holder concentration
  * [ ] abnormal transfer activity
* [ ] Output risk **signals with explanations** (no safe/unsafe)
* [ ] Basic confidence levels for signals
* [ ] API endpoint for contract analysis

---

### Web3 Website Risk Check (v0)

* [ ] URL input support
* [ ] Domain and SSL metadata checks
* [ ] Hosting and basic reputation signals
* [ ] Web3-specific checks

  * [ ] wallet interaction patterns
  * [ ] contract ↔ website mismatch
* [ ] Website risk signals with explanations

---

### Skill-Based Contract Auditing (v1)

* [ ] Define Skill interface (input, steps, output)
* [ ] Implement core audit Skills

  * [ ] contract structure understanding
  * [ ] permission analysis
  * [ ] asset flow analysis
* [ ] Replace one-shot audits with Skill pipelines
* [ ] Produce structured and reproducible audit output

---

### Agentic Code Checkers (v0)

* [ ] Convert existing code checkers into agents
* [ ] Adapt code checkers to run as Skills
* [ ] Allow checkers to:

  * [ ] request additional context
  * [ ] execute in sequence
  * [ ] reuse intermediate results
* [ ] Improve current checkers

  * [ ] reduce false negatives
  * [ ] reduce false positives
  * [ ] validate against real incidents
* [ ] Continue adding new code checkers

---

### Beta and Feedback

* [ ] Unified risk output format (contract, website, code)
* [ ] Internal or private beta
* [ ] Collect feedback on signal usefulness
* [ ] Track false positives and false negatives
* [ ] Collect real-world failure cases

---

## Month 2: Quality and Usability

### Signal and Checker Quality

* [ ] Improve signal weighting
* [ ] Reduce false positives across checkers
* [ ] Resolve known false negatives
* [ ] Add historical context to signals
* [ ] Improve confidence scoring

---

### More Skills and Checkers

* [ ] Governance attack detection
* [ ] Proxy and upgrade abuse analysis
* [ ] Tokenomics sanity checks
* [ ] Skill composition (Skill → Skill pipelines)
* [ ] Add more specialized code checkers

---

### On-Chain Intelligence

* [ ] Track historical rug pull patterns
* [ ] Compare new projects with known cases
* [ ] Basic behavior clustering

---

### Developer Experience

* [ ] API documentation
* [ ] Example integrations
* [ ] Webhook support for alerts
* [ ] Simple dashboard (optional)

---

### Platform Interaction

* [ ] Explore new interaction models for the platform
* [ ] Expose Skills and signals in more interactive ways
* [ ] Encourage users to:

  * [ ] submit cases
  * [ ] challenge results
  * [ ] contribute Skills or rules
* [ ] Use interaction data to guide future development

---

## Quarter Plan: Risk Intelligence System

### Skill and Agent System

* [ ] Shared Skill registry
* [ ] Multiple agents reusing Skills

  * [ ] contract agent
  * [ ] website agent
  * [ ] behavior agent
  * [ ] code analysis agent
* [ ] Cross-signal and cross-agent validation

---

### Threat Intelligence

* [ ] Known attacker pattern tracking
* [ ] Malicious domain fingerprints
* [ ] Reused contract component detection
* [ ] Continuous signal updates from real cases

---

### Ecosystem and Integration

* [ ] CI-based contract scanning
* [ ] Monitoring and alerting integrations
* [ ] Wallet and explorer integration exploration
* [ ] Browser extension (read-only alerts)

---

### Transparency and Community

* [ ] Publish real attack post-mortems
* [ ] Open-source selected Skills and checkers
* [ ] Accept external Skill and checker contributions

---

## Long-Term Direction

Chain-Fox is moving toward:

> A practical Web3 risk analysis and intelligence system,
> where code checkers, Skills, and agents work together,
> driven by real attacks and real user interaction,
> not one-shot LLM prompts.
