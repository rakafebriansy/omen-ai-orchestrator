# Graph Report - .  (2026-09-16)

## Corpus Check
- Corpus is ~43,476 words - fits in a single context window. You may not need a graph.

## Summary
- 44 nodes · 85 edges · 8 communities detected
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output
- Edge kinds: ON_BRANCH: 43 · PARENT_OF: 42


## Input Scope
- Requested: auto
- Resolved: committed (source: default-auto)
- Included files: 93 · Candidates: 109
- Excluded: 0 untracked · 0 ignored · 0 sensitive · 0 missing committed
- Recommendation: Use --scope all or graphify.yaml inputs.corpus for a knowledge-base folder.

## Graph Freshness
- Built from Git commit: `e9b5501`
- Compare this hash to `git rev-parse HEAD` before trusting freshness-sensitive graph output.
## God Nodes (most connected - your core abstractions)

## Surprising Connections (you probably didn't know these)
- `0e0c569 docs(global): enforce explicit global docs update on node scaling` --ON_BRANCH--> `main`  [EXTRACTED]
  git → git  _Bridges community 5 → community 0_
- `0e0c569 docs(global): enforce explicit global docs update on node scaling` --PARENT_OF--> `39b34b1 feat: implement dual operational modes and optional graphify`  [EXTRACTED]
  git → git  _Bridges community 5 → community 3_
- `1568986 docs: restructure main.md and consolidate guidelines hierarchy` --ON_BRANCH--> `main`  [EXTRACTED]
  git → git  _Bridges community 6 → community 0_
- `1568986 docs: restructure main.md and consolidate guidelines hierarchy` --PARENT_OF--> `20af9d8 docs: add changelog entry for main.md restruct and guidelines consolidation`  [EXTRACTED]
  git → git  _Bridges community 6 → community 2_
- `20af9d8 docs: add changelog entry for main.md restruct and guidelines consolidation` --ON_BRANCH--> `main`  [EXTRACTED]
  git → git  _Bridges community 2 → community 0_

## Communities

### Community 0 - "Community 0"
Cohesion: 0.35
Nodes (11): main, 1b2ad9f Initial commit, 288da8a docs: enforce strict SOP for AI agents in templates, 2ad929e feat(docs): migrate documentation diagrams from MermaidJS to PlantUML, 3c4ab46 docs: add single-project startup prompt to README, 6c75595 docs: add changelog template reference in startup prompt, 6d9eb62 Merge branch 'main' of https://github.com/rakafebriansy/ai-orchestrator-template, 9a86999 feat(docs): enforce CHANGELOG.md logging and Git commit/rollback mechanisms (+3 more)

### Community 1 - "Community 1"
Cohesion: 0.33
Nodes (6): 2c40006 docs(omen): initialize planning roadmap and modularize atomic tickets, 459b711 docs(omen): update design-system, tickets TICKET-03 and TICKET-04, and changelog for dual-theme landing, 51569d9 docs(omen): update changelog, ticket-04, and knowledge graph for landing page enhancements, 6b33964 docs(omen): enrich all backlog tickets with detailed UI and technical specifications, b6c178c docs(omen): complete TICKET-01 and update changelog, e9b5501 docs(omen): add anti-slop retrospective log and update changelog with logo prompt session

### Community 2 - "Community 2"
Cohesion: 0.40
Nodes (5): 20af9d8 docs: add changelog entry for main.md restruct and guidelines consolidation, 3cac701 docs(guideline): refine ai orchestrator terminology in version control rules, 832513b docs: enforce explicit git commit approval and ui prototyping ticket separation, a986005 feat: migrate graphify operations to path codebase and add pre-check SOP, f52b390 docs(template): update ticket, prd, design system, and guideline templates

### Community 3 - "Community 3"
Cohesion: 0.40
Nodes (5): 28b15f7 Update template retrospectives, 39b34b1 feat: implement dual operational modes and optional graphify, 43e25ef docs(guidelines): perjelas aturan pembuatan branch hanya di project/node, 754430b docs: update orchestrator guidelines for accessibility, testing, and branch switching, 80207fc docs(guidelines): add strict branch naming policy for nodes vs orchestrator

### Community 4 - "Community 4"
Cohesion: 0.40
Nodes (5): 5a0dd5c docs(orchestrator): resolve comprehensive audit report issues, 7230209 docs(template): update changelog entry format for prompt/autonomous modes and timestamp granularity, 868b9a4 docs(guidelines): add rule for state preservation and architectural integrity, 9a34d9f docs(guidelines): add pre-commit testing and linting rules, 9fae1bc docs(guideline): add detailed PR merge policy for AI agent

### Community 5 - "Community 5"
Cohesion: 0.50
Nodes (4): 0e0c569 docs(global): enforce explicit global docs update on node scaling, 29266e3 Update SOP for AI Execution and GitHub Projects integration, 55e64e4 docs(readme): add scaling prompt for adding new node, c6fa6b1 docs: tambahkan aturan auto-commit berbasis tiket ke SOP

### Community 6 - "Community 6"
Cohesion: 0.50
Nodes (4): 1568986 docs: restructure main.md and consolidate guidelines hierarchy, 252bc18 docs: update testing guidelines with 100% coverage requirement, 4d361ba docs: add test cleanup rule and strict git automation policy, cf68d7b docs(template): add mandatory implementation plan step to AI SOP

### Community 7 - "Community 7"
Cohesion: 0.50
Nodes (4): 411f24f docs(template): add implementation Q&A prompt and LEARN.md knowledge base, 5714c0d docs(template): add direct reference to changelog template in main.md, 625e08d docs(guideline): add database and datetime storage standard, b004144 docs(guidelines): add safe file operations policy and entrypoint references

## Suggested Questions
_Not enough signal to generate questions. This usually means the corpus has no AMBIGUOUS edges, no bridge nodes, no INFERRED relationships, and all communities are tightly cohesive. Add more files or run with --mode deep to extract richer edges._