# Graph Report - .  (2026-09-16)

## Corpus Check
- 96 files · ~79,044 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 85 nodes · 167 edges · 9 communities detected
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output
- Edge kinds: ON_BRANCH: 84 · PARENT_OF: 83


## Input Scope
- Requested: auto
- Resolved: committed (source: default-auto)
- Included files: 96 · Candidates: 112
- Excluded: 0 untracked · 0 ignored · 0 sensitive · 0 missing committed
- Recommendation: Use --scope all or graphify.yaml inputs.corpus for a knowledge-base folder.

## Graph Freshness
- Built from Git commit: `41745ae`
- Compare this hash to `git rev-parse HEAD` before trusting freshness-sensitive graph output.
## God Nodes (most connected - your core abstractions)

## Surprising Connections (you probably didn't know these)
- `046aa2f docs(omen): complete ticket-19 admin market create form ui and update changelog` --ON_BRANCH--> `main`  [EXTRACTED]
  git → git  _Bridges community 1 → community 0_
- `0ffa267 docs(omen): complete ticket-41 web3 claim payout wiring` --ON_BRANCH--> `main`  [EXTRACTED]
  git → git  _Bridges community 4 → community 0_
- `1568986 docs: restructure main.md and consolidate guidelines hierarchy` --ON_BRANCH--> `main`  [EXTRACTED]
  git → git  _Bridges community 3 → community 0_
- `2c40006 docs(omen): initialize planning roadmap and modularize atomic tickets` --ON_BRANCH--> `main`  [EXTRACTED]
  git → git  _Bridges community 5 → community 0_
- `30e1fc0 docs(omen): complete ticket-45 integrate omen brand logo and update changelog` --ON_BRANCH--> `main`  [EXTRACTED]
  git → git  _Bridges community 2 → community 0_

## Communities

### Community 0 - "Community 0"
Cohesion: 0.19
Nodes (20): main, 0e0c569 docs(global): enforce explicit global docs update on node scaling, 1b2ad9f Initial commit, 288da8a docs: enforce strict SOP for AI agents in templates, 28b15f7 Update template retrospectives, 29266e3 Update SOP for AI Execution and GitHub Projects integration, 2ad929e feat(docs): migrate documentation diagrams from MermaidJS to PlantUML, 39b34b1 feat: implement dual operational modes and optional graphify (+12 more)

### Community 1 - "Community 1"
Cohesion: 0.18
Nodes (11): 046aa2f docs(omen): complete ticket-19 admin market create form ui and update changelog, 1318a48 docs(omen): complete ticket-16 user bets table ui and update changelog, 5f78107 docs(omen): complete ticket-14 prediction markets feed page and update changelog, 6301d17 docs(omen): log robust admin login UI creation in changelog, 91c11b6 docs(omen): complete ticket-18 my bets page and update changelog, b7d6c11 docs(omen): log bet confirmation modal integration in changelog, bd9baf2 docs(omen): complete ticket-22 admin dashboard page UI, c024327 docs(omen): complete ticket-20 admin quest management form UI (+3 more)

### Community 2 - "Community 2"
Cohesion: 0.18
Nodes (11): 30e1fc0 docs(omen): complete ticket-45 integrate omen brand logo and update changelog, 51569d9 docs(omen): update changelog, ticket-04, and knowledge graph for landing page enhancements, 6008b82 docs(omen): complete ticket-08 quest card and sync changelog, 754eed6 docs(omen): complete ticket-13 prediction market card ui and update changelog, 8d44d29 docs(omen): complete ticket-11 points leaderboard page and update changelog, 9d9e35e docs(omen): complete ticket-12 market category filter ui and update changelog, b626b4e docs(omen): complete ticket-10 leaderboard table, add ticket-45 and sync changelog, bafaa9c docs(omen): complete ticket-05 connect wallet button and sync graphify (+3 more)

### Community 3 - "Community 3"
Cohesion: 0.22
Nodes (9): 1568986 docs: restructure main.md and consolidate guidelines hierarchy, 20af9d8 docs: add changelog entry for main.md restruct and guidelines consolidation, 252bc18 docs: update testing guidelines with 100% coverage requirement, 3cac701 docs(guideline): refine ai orchestrator terminology in version control rules, 4d361ba docs: add test cleanup rule and strict git automation policy, 832513b docs: enforce explicit git commit approval and ui prototyping ticket separation, a986005 feat: migrate graphify operations to path codebase and add pre-check SOP, cf68d7b docs(template): add mandatory implementation plan step to AI SOP (+1 more)

### Community 4 - "Community 4"
Cohesion: 0.25
Nodes (8): 0ffa267 docs(omen): complete ticket-41 web3 claim payout wiring, 320b955 docs(omen): complete ticket-31 api markets post create, b80683d docs(omen): complete ticket-39 web3 provider wagmi integration, d504c3f docs(omen): complete ticket-32 api markets resolve status, d599cfa docs(omen): complete ticket-33 api user bets get, e171064 docs(omen): complete ticket-34 api bets indexer, eb528f8 docs(omen): complete ticket-30 api markets get feed, f1a6310 docs(omen): complete ticket-40 web3 betting transaction wiring

### Community 5 - "Community 5"
Cohesion: 0.25
Nodes (8): 2c40006 docs(omen): initialize planning roadmap and modularize atomic tickets, 411f24f docs(template): add implementation Q&A prompt and LEARN.md knowledge base, 459b711 docs(omen): update design-system, tickets TICKET-03 and TICKET-04, and changelog for dual-theme landing, 5714c0d docs(template): add direct reference to changelog template in main.md, 625e08d docs(guideline): add database and datetime storage standard, 6b33964 docs(omen): enrich all backlog tickets with detailed UI and technical specifications, b004144 docs(guidelines): add safe file operations policy and entrypoint references, b6c178c docs(omen): complete TICKET-01 and update changelog

### Community 6 - "Community 6"
Cohesion: 0.25
Nodes (8): 3c4fc3b docs(omen): complete ticket-35 hardhat setup and arbitrum sepolia configuration, 8cf1f2a docs(admin): log production-ready admin dashboard overhaul, 9c0f1dd docs(omen): complete ticket-23 supabase schema migration, a13b16f docs(omen): log admin login UI viewport centering and aesthetic refinement, aed2407 docs(omen): complete ticket-25 api wallet connect upsert, c698ff4 docs(omen): complete ticket-36 prediction market contract implementation, fa18519 docs(omen): complete ticket-24 supabase database client helper, fdcde64 docs(omen): complete ticket-26 api daily checkin streak

### Community 7 - "Community 7"
Cohesion: 0.40
Nodes (5): 3dc9e9a docs(omen): complete ticket-28 api quest completion verification, 7cffa15 docs(omen): complete ticket-38 testnet deployment and abi export, afcd968 docs(omen): complete ticket-29 api points leaderboard, bc4d061 docs(omen): complete ticket-27 api quests list, ef3034d docs(omen): complete ticket-37 hardhat contract unit testing

### Community 8 - "Community 8"
Cohesion: 0.40
Nodes (5): 5a0dd5c docs(orchestrator): resolve comprehensive audit report issues, 7230209 docs(template): update changelog entry format for prompt/autonomous modes and timestamp granularity, 868b9a4 docs(guidelines): add rule for state preservation and architectural integrity, 9a34d9f docs(guidelines): add pre-commit testing and linting rules, 9fae1bc docs(guideline): add detailed PR merge policy for AI agent

## Suggested Questions
_Not enough signal to generate questions. This usually means the corpus has no AMBIGUOUS edges, no bridge nodes, no INFERRED relationships, and all communities are tightly cohesive. Add more files or run with --mode deep to extract richer edges._