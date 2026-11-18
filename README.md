# Collabrium skills

A curated catalog of free, open-source [Agent Skills](https://agentskills.io) for
[Collabrium](https://collabrium.si), the AI-native workspace by Falcon Tech Systems.

A skill is a folder with a `SKILL.md` (YAML frontmatter with `name` and `description`, then instructions in Markdown)
and, optionally, reference files, templates and scripts. An agent sees each skill's name and description, and reads the
rest only when a task calls for it.

Every skill here was written by someone else, published under a permissive open-source license, reviewed, and copied in
with its license and full attribution. Nothing here is original work except the glue (this README, the index, the
contributing guide).

## How Collabrium uses this repository

Collabrium's worker indexes the sources listed in its `SKILL_CATALOG_SOURCES` setting once a day (`skill-catalog-sync`).
Point it at this repository's `skills/` folder:

```
SKILL_CATALOG_SOURCES=Falcon-Tech-Systems/collabrium-skills/skills@main
```

(add `anthropics/skills` after a comma to keep Anthropic's catalog as well). The sync resolves `main` to a commit,
downloads that commit's tarball, and records every `skills/<folder>/SKILL.md` that parses: its name, description,
license, folder and commit. When someone adds a skill from the catalog, Collabrium downloads that exact commit again,
checks the folder against its limits, shows a review (files, scripts, risk indicators), and stores the files pinned to
their digest. Scripts in a skill only ever run in Collabrium's sandbox, through its tools and approvals.

What the importer expects, and what this repository keeps to:

- one folder per skill at `skills/<name>/`, holding a `SKILL.md` whose frontmatter `name` equals the folder name
  (1-64 characters of `a-z`, `0-9` and single hyphens, without `claude` or `anthropic`) and a `description` of at
  most 1,024 characters;
- no `SKILL.md` anywhere else in the repository, and no skill folder inside another;
- at most 512 files and 16 MiB per skill; the whole repository tarball must stay under 16 MiB (download cap) and
  unpack to under 25 MiB (it is about 1 MB / 2.5 MB today);
- no symlinks, hard links or special files, no `..` or absolute paths, no file names with invisible characters, paths
  at most 12 levels and 512 characters deep, `SKILL.md` under 256 KiB;
- no hidden (dot) files inside a skill folder;
- frontmatter `license` set to the SPDX id of the skill's license, so the catalog shows it.

## License policy

Each skill keeps its own license; the top-level [LICENSE](LICENSE) (MIT) covers only this repository's own files.

A skill is included only when its license clearly allows redistribution and modification: MIT, Apache-2.0,
BSD-2-Clause, BSD-3-Clause, ISC, CC0-1.0, Unlicense or CC-BY-4.0. Excluded: no license, copyleft (GPL, AGPL, LGPL,
MPL, CC-BY-SA), non-commercial or no-derivatives terms (CC-BY-NC, CC-BY-ND), source-available or proprietary terms,
and anything unclear (for example a folder with no license file in a repository with no top-level license).

For every skill:

- the original license text is in the skill's folder (`LICENSE` or `LICENSE.txt`), and upstream copyright headers are
  kept;
- `SOURCE.md` in the folder records the upstream repository, the exact commit, the original authors, the license, and
  every change made here;
- [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) lists the same for all skills; Apache-2.0 `NOTICE` files, where
  upstream has them, are carried in the skill folder and quoted there.

Skills are copied as they are. The only changes allowed are what it takes to fit the format above (adding the license
file and the `license` field, bundling a file the skill links to outside its folder), and each is recorded.

## Quality and safety bar

Skills are chosen for small-business teams: writing, research, meetings, planning, marketing, data, documentation,
design, coding, review, testing and git. A skill is left out when it is trivial, duplicates a better one here, is
broken (for example, it depends on files or skills that are not included), relies on a paid or proprietary service
without saying so, is tied to one company's internal conventions, or carries scripts that do anything questionable:
piping downloads into a shell, reading credentials, obfuscated code, telemetry, writing outside the working directory,
or turning off safety checks.

## Skills

The full index, with source commit and authors, is in [skills.json](skills.json).

### Writing and communication

| Skill | What it does | License | Source |
|---|---|---|---|
| [`copy-editing`](skills/copy-editing/) | When the user wants to edit, tighten, proofread, or refresh existing copy, or asks whether to keep, cut, or change a line in it, without rewriting from scratch… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`humanizer`](skills/humanizer/) | Rewrite AI-sounding text so it reads like the writer without changing what it says. Use when editing or reviewing prose for AI tells: not-X-but-Y contrasts, on… | MIT | [blader/humanizer](https://github.com/blader/humanizer) |
| [`internal-comms`](skills/internal-comms/) | A set of resources to help me write all kinds of internal communications, using the formats that my company likes to use. Claude should use this skill whenever… | Apache-2.0 | [anthropics/skills](https://github.com/anthropics/skills) |
| [`release-notes`](skills/release-notes/) | Generate user-facing release notes from tickets, PRDs, or changelogs. Creates clear, engaging summaries organized by category (new features, improvements, fixe… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |

### Documentation

| Skill | What it does | License | Source |
|---|---|---|---|
| [`documentation-and-adrs`](skills/documentation-and-adrs/) | Records decisions and documentation, and detects when documentation has drifted from the code it describes. Use when you need to document an architecture decis… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`markdown-mermaid-writing`](skills/markdown-mermaid-writing/) | Writes scientific Markdown documentation and Mermaid diagrams for workflows, relationships, timelines, and schemas. Provides syntax references, document templa… | Apache-2.0 | [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) |

### Meetings and team rituals

| Skill | What it does | License | Source |
|---|---|---|---|
| [`retro`](skills/retro/) | Facilitate a structured sprint retrospective — what went well, what didn't, and prioritized action items with owners and deadlines. Use when running a retrospe… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`summarize-meeting`](skills/summarize-meeting/) | Summarize a meeting transcript into structured notes with date, participants, topic, key decisions, summary points, and action items. Use when processing meeti… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |

### Research and customer insight

| Skill | What it does | License | Source |
|---|---|---|---|
| [`competitor-analysis`](skills/competitor-analysis/) | Analyze competitors with strengths, weaknesses, and differentiation opportunities. Identifies direct competitors and maps the competitive landscape. Use when d… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`customer-research`](skills/customer-research/) | When the user wants to run or synthesize customer research, or asks what customer quotes, reviews, or feedback really mean, what is safe to conclude, and what… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`discernment-nudge`](skills/discernment-nudge/) | After you give a substantive answer or draft that the user may act on — advice or recommendations, drafted artifacts such as goals, plans, pitches, proposals,… | Apache-2.0 | [anthropics/skills](https://github.com/anthropics/skills) |
| [`interview-script`](skills/interview-script/) | Create a structured customer interview script with JTBD probing questions, warm-up, core exploration, and wrap-up sections. Follows The Mom Test principles — n… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`summarize-interview`](skills/summarize-interview/) | Summarize a customer interview transcript into a structured template with JTBD, satisfaction signals, and action items. Use when processing interview recording… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`survey-design`](skills/survey-design/) | Writing or reviewing a survey or questionnaire: customer feedback, NPS, CSAT, CES, pricing, market research, an in-app survey. Starts from the decision, asks a… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`user-personas`](skills/user-personas/) | Create refined user personas from research data — 3 personas with JTBD, pains, gains, and unexpected insights. Use when building personas from survey data, cre… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |

### Strategy

| Skill | What it does | License | Source |
|---|---|---|---|
| [`swot-analysis`](skills/swot-analysis/) | Perform a detailed SWOT analysis — strengths, weaknesses, opportunities, and threats with actionable recommendations. Use when doing strategic assessment, comp… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |

### Planning and product

| Skill | What it does | License | Source |
|---|---|---|---|
| [`brainstorm-okrs`](skills/brainstorm-okrs/) | Brainstorm team-level OKRs aligned with company objectives — qualitative objectives with measurable key results. Use when setting quarterly OKRs, aligning team… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`create-prd`](skills/create-prd/) | Create a lean, decision-ready Product Requirements Document with an 8-section template: summary, contacts, background, objective, market segments, value propos… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`idea-refine`](skills/idea-refine/) | Refines raw ideas into sharp, actionable concepts through structured divergent and convergent thinking. Use when an idea is still vague, when you need to stres… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`planning-and-task-breakdown`](skills/planning-and-task-breakdown/) | Breaks work into ordered tasks. Use when you have a spec or clear requirements and need to break work into implementable tasks. Use when a task feels too large… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`pre-mortem`](skills/pre-mortem/) | Run a pre-mortem risk analysis on a PRD or launch plan. Categorizes risks as Tigers (real problems), Paper Tigers (overblown concerns), and Elephants (unspoken… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`prioritization-frameworks`](skills/prioritization-frameworks/) | Reference guide to 9 prioritization frameworks with formulas, when-to-use guidance, and templates — RICE, ICE, Kano, MoSCoW, Opportunity Score, and more. Use w… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`shipping-and-launch`](skills/shipping-and-launch/) | Prepares production launches. Use when preparing to deploy to production, or when asking what needs to be in place before shipping. Use when you need a pre-lau… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`spec-driven-development`](skills/spec-driven-development/) | Creates specs before coding. Use when starting a new project, feature, or significant change and no specification exists yet. Use when drafting a PRD or requir… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`stakeholder-map`](skills/stakeholder-map/) | Build a stakeholder map using a power/interest grid, identify communication strategies per quadrant, and generate a communication plan. Use when managing stake… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`user-stories`](skills/user-stories/) | Create user stories following the 3 C's (Card, Conversation, Confirmation) and INVEST criteria with descriptions, design links, and acceptance criteria. Use wh… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |

### Marketing

| Skill | What it does | License | Source |
|---|---|---|---|
| [`content-strategy`](skills/content-strategy/) | When the user wants to plan content, or asks which topic or piece to prioritize, what to write about, or why posts bring no customers: topic clusters, editoria… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`copywriting`](skills/copywriting/) | When the user wants to write or rewrite page copy (homepage, landing, pricing, feature), or asks which headline, promise, or message to lead with. Diagnoses th… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`emails`](skills/emails/) | When the user wants to create or improve automated email sequences, or asks what to send, when, or whether an email or flow is working: welcome, onboarding, nu… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`launch`](skills/launch/) | When the user wants to plan a product or feature launch, or asks whether it's ready, when to announce, or how to get noticed: Product Hunt, beta and early acce… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`marketing-plan`](skills/marketing-plan/) | When the user wants a full marketing or go-to-market plan for a client, an advised company, or their own product, or asks how to sequence or prioritize several… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`pricing`](skills/pricing/) | When the user wants to set pricing and packaging, or asks what to charge, whether to raise prices, or how to move existing customers: tiers, value metrics, per… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`product-marketing`](skills/product-marketing/) | When the user wants to create or update the product marketing context doc (.agents/product-marketing.md), or asks what belongs in it or whether positioning or… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`seo-audit`](skills/seo-audit/) | When the user wants to audit or diagnose SEO, or asks why traffic dropped, a page won't rank, or whether a setup like canonicals, hreflang, or redirects is rig… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |
| [`social`](skills/social/) | When the user wants organic social content for LinkedIn, X, Instagram, TikTok, or Facebook, or asks what to post, which format to favor, or from which account:… | MIT | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) |

### Data analysis

| Skill | What it does | License | Source |
|---|---|---|---|
| [`sql-queries`](skills/sql-queries/) | Generate SQL queries from natural language descriptions. Supports BigQuery, PostgreSQL, MySQL, and other dialects. Reads database schemas from uploaded diagram… | MIT | [phuryn/pm-skills](https://github.com/phuryn/pm-skills) |
| [`statistical-analysis`](skills/statistical-analysis/) | Guided statistical analysis for research data - test selection, assumption checking, effect sizes, power analysis, Bayesian alternatives, and APA-formatted rep… | MIT | [K-Dense-AI/scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) |

### Design

| Skill | What it does | License | Source |
|---|---|---|---|
| [`frontend-design`](skills/frontend-design/) | Guidance for distinctive, intentional visual design when building new UI or reshaping an existing one. Helps with aesthetic direction, typography, and making c… | Apache-2.0 | [anthropics/skills](https://github.com/anthropics/skills) |
| [`theme-factory`](skills/theme-factory/) | Toolkit for styling artifacts with a theme. These artifacts can be slides, docs, reportings, HTML landing pages, etc. There are 10 pre-set themes with colors/f… | Apache-2.0 | [anthropics/skills](https://github.com/anthropics/skills) |

### Coding and review

| Skill | What it does | License | Source |
|---|---|---|---|
| [`api-and-interface-design`](skills/api-and-interface-design/) | Guides stable API and interface design. Use when designing APIs, module boundaries, or any public interface. Use when creating REST or GraphQL endpoints, defin… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`code-review-and-quality`](skills/code-review-and-quality/) | Conducts multi-axis code review. Use before merging any change. Use when reviewing code written by yourself, another agent, or a human. Use when you need to as… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`code-simplification`](skills/code-simplification/) | Simplifies code for clarity. Use when refactoring code for clarity without changing behavior. Use when code works but is harder to read, maintain, or extend th… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`incremental-implementation`](skills/incremental-implementation/) | Delivers changes incrementally in thin, verifiable slices. Use when implementing any feature or change that touches more than one file, or when picking up the… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`mcp-builder`](skills/mcp-builder/) | Guide for creating high-quality MCP (Model Context Protocol) servers that enable LLMs to interact with external services through well-designed tools. Use when… | Apache-2.0 | [anthropics/skills](https://github.com/anthropics/skills) |
| [`performance-optimization`](skills/performance-optimization/) | Optimizes application performance across frontend, backend, queries, and databases. Use when performance requirements exist, when you suspect performance regre… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`receiving-code-review`](skills/receiving-code-review/) | Use when receiving code review feedback, before implementing suggestions, especially if feedback seems unclear or technically questionable - requires technical… | MIT | [obra/superpowers](https://github.com/obra/superpowers) |
| [`requesting-code-review`](skills/requesting-code-review/) | Use when completing tasks, implementing major features, or before merging to verify work meets requirements | MIT | [obra/superpowers](https://github.com/obra/superpowers) |
| [`security-and-hardening`](skills/security-and-hardening/) | Hardens code against vulnerabilities. Use when auditing an input handler for vulnerabilities, when handling user input, authentication, data storage, or extern… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`systematic-debugging`](skills/systematic-debugging/) | Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes | MIT | [obra/superpowers](https://github.com/obra/superpowers) |
| [`verification-before-completion`](skills/verification-before-completion/) | Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output b… | MIT | [obra/superpowers](https://github.com/obra/superpowers) |

### Testing

| Skill | What it does | License | Source |
|---|---|---|---|
| [`test-driven-development`](skills/test-driven-development/) | Use when implementing any feature or bugfix, before writing implementation code | MIT | [obra/superpowers](https://github.com/obra/superpowers) |
| [`webapp-testing`](skills/webapp-testing/) | Toolkit for interacting with and testing local web applications using Playwright. Supports verifying frontend functionality, debugging UI behavior, capturing b… | Apache-2.0 | [anthropics/skills](https://github.com/anthropics/skills) |

### Git

| Skill | What it does | License | Source |
|---|---|---|---|
| [`finishing-a-development-branch`](skills/finishing-a-development-branch/) | Use when implementation is complete, all tests pass, and you need to decide how to integrate the work | MIT | [obra/superpowers](https://github.com/obra/superpowers) |
| [`git-workflow-and-versioning`](skills/git-workflow-and-versioning/) | Structures git workflow practices. Use when making any code change. Use when committing, branching, resolving conflicts, splitting uncommitted work in a messy… | MIT | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) |
| [`using-git-worktrees`](skills/using-git-worktrees/) | Use when starting feature work that needs isolation from current workspace or before executing implementation plans - ensures an isolated workspace exists via… | MIT | [obra/superpowers](https://github.com/obra/superpowers) |

### Skills and prompts

| Skill | What it does | License | Source |
|---|---|---|---|
| [`prompt-optimizer`](skills/prompt-optimizer/) | Creates, optimizes, and iteratively refines agent prompts, system prompts, developer prompts, and reusable prompt templates. Use when asked to improve a prompt… | Apache-2.0 | [getsentry/skills](https://github.com/getsentry/skills) |
| [`skill-creator`](skills/skill-creator/) | Create new skills, modify and improve existing skills, and measure skill performance. Use when users want to create a skill from scratch, edit, or optimize an… | Apache-2.0 | [anthropics/skills](https://github.com/anthropics/skills) |

## Adding a skill

See [CONTRIBUTING.md](CONTRIBUTING.md). In short: find a skill under an allowed license, read every file in it, copy
the folder to `skills/<name>/` with its license text and a `SOURCE.md`, add it to `skills.json`, the table above and
`THIRD_PARTY_NOTICES.md`, and check it imports in Collabrium (Skills, then Add from GitHub, with
`Falcon-Tech-Systems/collabrium-skills/skills/<name>@<your-branch>`) before opening a pull request.

## Considered and left out

So no one has to re-check them. These are the notable ones; the reasons apply as of 2026-11-18.

| Skill(s) | Source | Why left out |
|---|---|---|
| `docx`, `pdf`, `pptx`, `xlsx` | anthropics/skills | Anthropic's document skills, long published as source-available. Upstream now labels them Apache-2.0, but they stay out until Falcon Tech Systems decides otherwise. Copies of them in other repositories are left out for the same reason. |
| `doc-coauthoring` | anthropics/skills, getsentry/skills | Anthropic's folder has no license file and the repository has no top-level license, so the license is unclear. Sentry's copy is adapted from it. |
| `brand-guidelines`, `academy-guide`, `claude-api` | anthropics/skills | Specific to Anthropic's own brand and products. |
| `canvas-design`, `slack-gif-creator`, `algorithmic-art`, `web-artifacts-builder` | anthropics/skills | Bundled font binaries; niche; a prebuilt tarball and a claude.ai-only output target. |
| `brainstorming` | obra/superpowers | Its visual companion writes session files to `/tmp` by default and loads a remote logo image. |
| `executing-plans`, `subagent-driven-development`, `dispatching-parallel-agents`, `using-superpowers`, `writing-skills` | obra/superpowers | Depend on each other's scripts or on one agent harness's subagent tool; framework meta-skills. |
| `security-review` | getsentry/skills | Its reference material is CC-BY-SA-4.0 (share-alike). |
| most of `getsentry/skills` | getsentry/skills | Tied to Sentry's own repository conventions and branding. |
| all | trailofbits/skills | CC-BY-SA-4.0 (share-alike). |
| all | vercel-labs/agent-skills, openai/skills, ComposioHQ/awesome-claude-skills | No license on the repository. |
| `grill-me`, `handoff`, `to-spec`, … | mattpocock/skills | MIT, but mostly very short, or tied to the author's own issue-tracker setup. |
| `polars`, `matplotlib` and others | K-Dense-AI/scientific-agent-skills | The `license` field points at the wrapped library's license, so the license of the skill text is unclear. Most skills there are for scientific research. |
