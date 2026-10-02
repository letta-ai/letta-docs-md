---
title: Changelog | Letta Docs
description: Release notes and version history for Letta Code
applies_to:
  backends:
    - cloud
    - local
  interfaces:
    - web
    - desktop
    - cli
    - sdk
---

Notable changes to Letta Code are documented here. Documentation may be delayed - for a fully up-to-date reference, check the Letta Code [GitHub releases page](https://github.com/letta-ai/letta-code/releases).

**Historical terminology: Constellation**

Letta Code versions 0.26.0 through 0.28.13 used **Constellation** for cloud-hosted agents and related sign-in and backend UI. The terminology was retired after 0.28.13 ([#3431](https://github.com/letta-ai/letta-code/pull/3431)). See [Terminology](/reference/terminology#constellation/index.md) for current equivalents.

## 0.33.2

- Added schema validation for Workflow agent results ([#4707](https://github.com/letta-ai/letta-code/pull/4707))
- Improved memory initialization using workflow analysis ([#4643](https://github.com/letta-ai/letta-code/pull/4643))
- Fixed unbounded harness log growth with size caps, managed Cloud schedule durability, and Cloud message enqueue retries after shutdown rejection ([#4696](https://github.com/letta-ai/letta-code/pull/4696), [#4722](https://github.com/letta-ai/letta-code/pull/4722), [#4728](https://github.com/letta-ai/letta-code/pull/4728))
- Removed tools that were outside the toolset catalog ([#4603](https://github.com/letta-ai/letta-code/pull/4603))

## 0.33.1

- Added Claude Code and Codex subagent workers, the Wake tool for timed follow-ups, and structured-output support display and filtering in the model selector ([#4694](https://github.com/letta-ai/letta-code/pull/4694), [#4704](https://github.com/letta-ai/letta-code/pull/4704), [#4703](https://github.com/letta-ai/letta-code/pull/4703))
- Fixed composer input history growth (now capped at 500 entries), cloud tool-return clipping in transcripts, acting-user identity preservation after teleport, steering-message acknowledgment, replies landing before the next tool call, SDK tool availability in agent-free turns, model overrides in new headless conversations, launch-time credential retention for tool-output redaction, and empty acting-user telemetry snapshots ([#4661](https://github.com/letta-ai/letta-code/pull/4661), [#4675](https://github.com/letta-ai/letta-code/pull/4675), [#4681](https://github.com/letta-ai/letta-code/pull/4681), [#4702](https://github.com/letta-ai/letta-code/pull/4702), [#4708](https://github.com/letta-ai/letta-code/pull/4708), [#4709](https://github.com/letta-ai/letta-code/pull/4709), [#4699](https://github.com/letta-ai/letta-code/pull/4699), [#4714](https://github.com/letta-ai/letta-code/pull/4714), [#4706](https://github.com/letta-ai/letta-code/pull/4706))
- Improved agent coordination focus and reduced the web bundle by keeping the diff viewer external to `letta.js` ([#4700](https://github.com/letta-ai/letta-code/pull/4700), [#4685](https://github.com/letta-ai/letta-code/pull/4685))
- Removed the dispatching-coding-agents builtin skill ([#4715](https://github.com/letta-ai/letta-code/pull/4715))

## 0.33.0

- Added a background worker for incidental memory upkeep and post-turn Git-conflict repair, and exposed running workflows through the protocol ([#4628](https://github.com/letta-ai/letta-code/pull/4628), [#4634](https://github.com/letta-ai/letta-code/pull/4634), [#4652](https://github.com/letta-ai/letta-code/pull/4652))
- Fixed preservation of effort-suffixed model pins at subagent spawn and redaction of ambient runtime credentials in tool output ([#4663](https://github.com/letta-ai/letta-code/pull/4663), [#4657](https://github.com/letta-ai/letta-code/pull/4657))

## 0.32.19

- Added live workflow status rows under the input ([#4583](https://github.com/letta-ai/letta-code/pull/4583))
- Fixed installations by pinning a compatible Ink runtime ([#4653](https://github.com/letta-ai/letta-code/pull/4653))
- Improved memory usage by keeping tool output line buffers only for Bash ([#4646](https://github.com/letta-ai/letta-code/pull/4646))

## 0.32.18

- Added Claude Opus 5.5 model support ([#4642](https://github.com/letta-ai/letta-code/pull/4642))
- Changed the TUI to hide system reminders and collapse thinking by default ([#4032](https://github.com/letta-ai/letta-code/pull/4032))
- Improved agent memory: new Cloud agents are created on the MemFS v2 root layout, concurrent harness writes to a memory checkout are serialized, and delegated memory upkeep runs in a silent background worker ([#4644](https://github.com/letta-ai/letta-code/pull/4644), [#4626](https://github.com/letta-ai/letta-code/pull/4626), [#4627](https://github.com/letta-ai/letta-code/pull/4627))
- Fixed Cloud system prompt default inheritance, subagent initial input IDs and SendAgentMessage child tracking, missing image-resize worker reporting, OpenAI toolset detection by provider type, and GPT-6 Sol/Luna none-effort and GPT-6 max-effort recognition ([#4611](https://github.com/letta-ai/letta-code/pull/4611), [#4617](https://github.com/letta-ai/letta-code/pull/4617), [#4616](https://github.com/letta-ai/letta-code/pull/4616), [#4596](https://github.com/letta-ai/letta-code/pull/4596), [#4607](https://github.com/letta-ai/letta-code/pull/4607), [#4631](https://github.com/letta-ai/letta-code/pull/4631))

## 0.32.16

- Changed startup to default to the Cloud backend ([#4584](https://github.com/letta-ai/letta-code/pull/4584))
- Added subagent launching from App Server clients and a CLI report of configured agent permissions, including peer names ([#4606](https://github.com/letta-ai/letta-code/pull/4606), [#4609](https://github.com/letta-ai/letta-code/pull/4609), [#4615](https://github.com/letta-ai/letta-code/pull/4615))
- Fixed client notifications after post-turn memory pushes, truncated MCP CLI output, and local schedules running on the local listener ([#4592](https://github.com/letta-ai/letta-code/pull/4592), [#4553](https://github.com/letta-ai/letta-code/pull/4553), [#4161](https://github.com/letta-ai/letta-code/pull/4161))
- Removed the BYOK triangle indicator from the prompt footer ([#4608](https://github.com/letta-ai/letta-code/pull/4608))

## 0.32.15

- Changed the Workflow tool to a thin wrapper around the Agent SDK `query()` ([#4531](https://github.com/letta-ai/letta-code/pull/4531))
- Added structured output schema forwarding in the App Server protocol ([#4586](https://github.com/letta-ai/letta-code/pull/4586))

## 0.32.14

- Added Grok OAuth sign-in for Cloud agents and subscription OAuth token support on `connect_provider` ([#4543](https://github.com/letta-ai/letta-code/pull/4543), [#4547](https://github.com/letta-ai/letta-code/pull/4547))
- Added a warning for Windows agents against redirecting native stderr in Bash tool commands ([#4511](https://github.com/letta-ai/letta-code/pull/4511))
- Changed `/dream` and `/reflect` to route by reflection ownership, kept the model selector’s ten most recent models, and aligned tool overflow output with Claude ([#4450](https://github.com/letta-ai/letta-code/pull/4450), [#4542](https://github.com/letta-ai/letta-code/pull/4542), [#4537](https://github.com/letta-ai/letta-code/pull/4537))
- Improved first-run registration: no name prompt, the sign-in page opens automatically, and the computer points back at the browser once registered ([#4538](https://github.com/letta-ai/letta-code/pull/4538), [#4554](https://github.com/letta-ai/letta-code/pull/4554))
- Removed the `/remember` command, the Gemini and codex\_snake toolsets, and the shadow suffix from generated subagent names ([#4525](https://github.com/letta-ai/letta-code/pull/4525), [#4506](https://github.com/letta-ai/letta-code/pull/4506), [#4546](https://github.com/letta-ai/letta-code/pull/4546))
- Fixed headless response-state reuse for automatic tool continuations and remote startup authorization as the sender ([#4524](https://github.com/letta-ai/letta-code/pull/4524), [#4530](https://github.com/letta-ai/letta-code/pull/4530))
- Fixed `letta memory pull` settings initialization, multiline YAML skill descriptions, stream sequence cursors leaking across runs, pasted multi-read input commits, monitors lost across turn interrupts, reflection sandbox failure semantics, streamed assistant identities in local mode, worktree creation with repository checkout filters, and agent IDs in fork and recall launch receipts ([#4500](https://github.com/letta-ai/letta-code/pull/4500), [#4516](https://github.com/letta-ai/letta-code/pull/4516), [#4528](https://github.com/letta-ai/letta-code/pull/4528), [#4517](https://github.com/letta-ai/letta-code/pull/4517), [#4548](https://github.com/letta-ai/letta-code/pull/4548), [#4527](https://github.com/letta-ai/letta-code/pull/4527), [#4329](https://github.com/letta-ai/letta-code/pull/4329), [#4509](https://github.com/letta-ai/letta-code/pull/4509), [#4557](https://github.com/letta-ai/letta-code/pull/4557))

## 0.32.13

- Added self-contained Python wheels as an install option ([#4518](https://github.com/letta-ai/letta-code/pull/4518))
- Fixed agent discovery as the current sender, process tree termination for stopped subagents, MemFS attached sync on the local backend, channel gateway restarts after unexpected exits, and restored the local ChatGPT reasoning picker ([#4483](https://github.com/letta-ai/letta-code/pull/4483), [#4497](https://github.com/letta-ai/letta-code/pull/4497), [#4504](https://github.com/letta-ai/letta-code/pull/4504), [#4478](https://github.com/letta-ai/letta-code/pull/4478), [#4474](https://github.com/letta-ai/letta-code/pull/4474))

## 0.32.12

- Added `letta usage` to show credits and model quota ([#4481](https://github.com/letta-ai/letta-code/pull/4481))
- Fixed listener recovery across Cloud API deployment interruptions, Desktop credential forwarding to subagent launches, stale Slack status writes and relinquishment, and blocked source input after a teleport disconnect before handoff ([#3875](https://github.com/letta-ai/letta-code/pull/3875), [#4486](https://github.com/letta-ai/letta-code/pull/4486), [#4461](https://github.com/letta-ai/letta-code/pull/4461), [#4299](https://github.com/letta-ai/letta-code/pull/4299))
- Removed the obsolete MCP conversion skill ([#4484](https://github.com/letta-ai/letta-code/pull/4484))

## 0.32.11

- Changed subagent naming so subagents are named as their parent’s shadows ([#4458](https://github.com/letta-ai/letta-code/pull/4458))
- Renamed the channel routing config from `routing.yaml` to `routing.json` with automatic migration from legacy files ([#3232](https://github.com/letta-ai/letta-code/pull/3232))
- Fixed shared memory repository cloning blocking startup, MemFS Git retries on HTTP 503 failures, App Server heartbeat probe counting, schedules preserving the requesting user, subagent task sender identification, configuration loss during ChatGPT account rotation, remote completion notifications, explicit pi-ai sampling options in local mode, routed tool ownership, and teleport resume when the source ends its turn ([#4438](https://github.com/letta-ai/letta-code/pull/4438), [#4463](https://github.com/letta-ai/letta-code/pull/4463), [#4291](https://github.com/letta-ai/letta-code/pull/4291), [#4456](https://github.com/letta-ai/letta-code/pull/4456), [#4471](https://github.com/letta-ai/letta-code/pull/4471), [#4451](https://github.com/letta-ai/letta-code/pull/4451), [#4466](https://github.com/letta-ai/letta-code/pull/4466), [#4455](https://github.com/letta-ai/letta-code/pull/4455), [#4473](https://github.com/letta-ai/letta-code/pull/4473), [#4477](https://github.com/letta-ai/letta-code/pull/4477))

## 0.32.10

- Fixed resuming locally recorded work after a process restart and teleport runtime reminders now delivered as user messages ([#4444](https://github.com/letta-ai/letta-code/pull/4444), [#4448](https://github.com/letta-ai/letta-code/pull/4448))

## 0.32.9

- Added curated agent names drawn from Fallout, Dune, and sci-fi classics ([#4441](https://github.com/letta-ai/letta-code/pull/4441))
- Fixed interrupted-turn resume to run only on the execution owner, included the conversation ID in background Task returns, handled secrets rejection during startup, and narrowed letta-guide self-configuration triggers ([#4431](https://github.com/letta-ai/letta-code/pull/4431), [#4440](https://github.com/letta-ai/letta-code/pull/4440), [#4443](https://github.com/letta-ai/letta-code/pull/4443), [#4446](https://github.com/letta-ai/letta-code/pull/4446))

## 0.32.8

- Added distinct sci-fi names for new subagents ([#4416](https://github.com/letta-ai/letta-code/pull/4416))
- Fixed message request retries when a gateway returns an HTML page, approval UI crashes from malformed questions, rejection of sends to the current conversation, teleport ownership during approval recovery, and queued messages stuck behind sender holds ([#4419](https://github.com/letta-ai/letta-code/pull/4419), [#4422](https://github.com/letta-ai/letta-code/pull/4422), [#4425](https://github.com/letta-ai/letta-code/pull/4425), [#4426](https://github.com/letta-ai/letta-code/pull/4426), [#4423](https://github.com/letta-ai/letta-code/pull/4423))

## 0.32.7

- Fixed optional computer value handling in CLI and tool message sends, startup recovery racing an active teleport handoff, and stale approvals being auto-finished on a teleport destination ([#4409](https://github.com/letta-ai/letta-code/pull/4409), [#4408](https://github.com/letta-ai/letta-code/pull/4408), [#4410](https://github.com/letta-ai/letta-code/pull/4410))

## 0.32.6

- Added readable agent message receipts in the TUI ([#4403](https://github.com/letta-ai/letta-code/pull/4403))
- Fixed interrupted-turn resume after restarts, with retries across a cloud-api restart and resume on the first sync ([#4401](https://github.com/letta-ai/letta-code/pull/4401), [#4404](https://github.com/letta-ai/letta-code/pull/4404))

## 0.32.5

- Fixed MCP attachments to refresh before each turn ([#4398](https://github.com/letta-ai/letta-code/pull/4398))

## 0.32.4

- Added Cloud message enqueueing with a `--no-wait` flag, the SendAgentMessage tool for agent coordination, and doctor investigation of agent behavior from conversation evidence ([#4383](https://github.com/letta-ai/letta-code/pull/4383), [#4392](https://github.com/letta-ai/letta-code/pull/4392), [#4375](https://github.com/letta-ai/letta-code/pull/4375))
- Fixed conversation monitors not cancelling on interrupt, resuming teleported turns after reconnect, child agents running through their listener, and message steering blocked by background notifications ([#4377](https://github.com/letta-ai/letta-code/pull/4377), [#4384](https://github.com/letta-ai/letta-code/pull/4384), [#4389](https://github.com/letta-ai/letta-code/pull/4389), [#4391](https://github.com/letta-ai/letta-code/pull/4391))

## 0.32.3

- Added sandbox file transfer targeting for another conversation and simplified sandbox targeting with cross-computer guidance ([#4370](https://github.com/letta-ai/letta-code/pull/4370), [#4371](https://github.com/letta-ai/letta-code/pull/4371))
- Fixed flickering parallel tool status titles and lost activity status in Slack, duplicate computer listeners, queued senders leaking into active continuations, and image-generation credits reported only when asked ([#4376](https://github.com/letta-ai/letta-code/pull/4376), [#4380](https://github.com/letta-ai/letta-code/pull/4380), [#4378](https://github.com/letta-ai/letta-code/pull/4378), [#4379](https://github.com/letta-ai/letta-code/pull/4379), [#4382](https://github.com/letta-ai/letta-code/pull/4382))

## 0.32.2

- Added host-provided Slack conversation binding actions and an experimental unified Letta toolset ([#4358](https://github.com/letta-ai/letta-code/pull/4358), [#4217](https://github.com/letta-ai/letta-code/pull/4217))
- Removed the deprecated AgentFile import and export commands ([#4354](https://github.com/letta-ai/letta-code/pull/4354))
- Fixed subagent retries losing memoryScope when a provider is unsupported, reflection losing full tool call arguments, agent-limit errors now linking to Chat, unfinished requests lost across queued messages, and queued turn separation by acting user ([#4205](https://github.com/letta-ai/letta-code/pull/4205), [#4087](https://github.com/letta-ai/letta-code/pull/4087), [#4356](https://github.com/letta-ai/letta-code/pull/4356), [#4331](https://github.com/letta-ai/letta-code/pull/4331), [#4357](https://github.com/letta-ai/letta-code/pull/4357))

## 0.32.1

- Added `letta model` get, list, and set commands ([#4339](https://github.com/letta-ai/letta-code/pull/4339))
- Improved headless `--computer` routing to infer the ambient agent, agent notifications when available skills change, and proactive learning from human feedback ([#4343](https://github.com/letta-ai/letta-code/pull/4343), [#4330](https://github.com/letta-ai/letta-code/pull/4330), [#4346](https://github.com/letta-ai/letta-code/pull/4346))
- Fixed OpenCode Go session headers, agent tag and memory block retrieval, catalog and BYOK model selection in Slack, teleport Cloud destinations staying API-backed, ChatGPT plan rotation skipping exhausted plans, subagent acting user preservation, and rejection of local channel moves at the teleport source ([#4290](https://github.com/letta-ai/letta-code/pull/4290), [#4341](https://github.com/letta-ai/letta-code/pull/4341), [#4340](https://github.com/letta-ai/letta-code/pull/4340), [#4344](https://github.com/letta-ai/letta-code/pull/4344), [#4342](https://github.com/letta-ai/letta-code/pull/4342), [#4334](https://github.com/letta-ai/letta-code/pull/4334), [#4347](https://github.com/letta-ai/letta-code/pull/4347))

## 0.32.0

- Added default MemFS v2 budget enforcement and renewed Desktop credential acceptance without restarting ([#4185](https://github.com/letta-ai/letta-code/pull/4185), [#4309](https://github.com/letta-ai/letta-code/pull/4309))
- Changed interrupt handling to park queued user messages, with `resume_queue` to resume them ([#4213](https://github.com/letta-ai/letta-code/pull/4213))
- Fixed teleport channel-bound moves until MessageChannel can follow, Slack commands handled before thread routing, LS relative paths resolved from the runtime working directory, background tracking of GitHub PR commands that hit a timeout, Esc interrupts draining queued notifications, and streamed quota errors retained for ChatGPT plan rotation ([#4223](https://github.com/letta-ai/letta-code/pull/4223), [#4306](https://github.com/letta-ai/letta-code/pull/4306), [#4298](https://github.com/letta-ai/letta-code/pull/4298), [#4285](https://github.com/letta-ai/letta-code/pull/4285), [#4201](https://github.com/letta-ai/letta-code/pull/4201), [#4317](https://github.com/letta-ai/letta-code/pull/4317))

## 0.31.14

- Added the ability to cancel Monitors from connected clients ([#4280](https://github.com/letta-ai/letta-code/pull/4280))
- Fixed memory refreshes during reflection prompting for credentials and added backoff for failed memory integration retries ([#4277](https://github.com/letta-ai/letta-code/pull/4277), [#4276](https://github.com/letta-ai/letta-code/pull/4276))
- Fixed forwarded Discord messages not being delivered ([#4212](https://github.com/letta-ai/letta-code/pull/4212))
- Improved model provider compatibility by upgrading pi-ai to 0.85.1 ([#4237](https://github.com/letta-ai/letta-code/pull/4237))

## 0.31.13

- Added Slack workspace custom emoji discovery, the hidden `clear-messages` command, notifications when yielded exec commands finish, automatic backgrounding of slow Bash commands, and an official Docker Hub container image ([#4203](https://github.com/letta-ai/letta-code/pull/4203), [#4215](https://github.com/letta-ai/letta-code/pull/4215), [#4219](https://github.com/letta-ai/letta-code/pull/4219), [#4220](https://github.com/letta-ai/letta-code/pull/4220), [#4260](https://github.com/letta-ai/letta-code/pull/4260))
- Fixed operational logs leaking into the status UI, MiniMax BYOK reasoning tier resolution, subagent default conversations resuming with the wrong agent ID, and Monitor tool descriptions ([#4209](https://github.com/letta-ai/letta-code/pull/4209), [#4184](https://github.com/letta-ai/letta-code/pull/4184), [#4228](https://github.com/letta-ai/letta-code/pull/4228), [#4268](https://github.com/letta-ai/letta-code/pull/4268))
- Changed the minimum supported runtime to Bun 1.3.2 ([#4231](https://github.com/letta-ai/letta-code/pull/4231))
- Improved API and listener efficiency by coalescing in-flight agent retrievals and loading device Git status asynchronously ([#4208](https://github.com/letta-ai/letta-code/pull/4208), [#4230](https://github.com/letta-ai/letta-code/pull/4230))

## 0.31.12

- Changed remote routing to standardize on computers and routed client-local MCP tools through the unified CLI ([#4194](https://github.com/letta-ai/letta-code/pull/4194), [#4182](https://github.com/letta-ai/letta-code/pull/4182))
- Fixed behavioral corrections being submitted as product feedback instead of memory edits, and ChatGPT plan rotation applying beyond the active turn ([#4190](https://github.com/letta-ai/letta-code/pull/4190), [#4202](https://github.com/letta-ai/letta-code/pull/4202))

## 0.31.11

- Added MCP tool discoverability through the using-mcp-tools skill, an MCP servers reminder, and `letta mcp` search and schema commands, plus source and client metadata on agent feedback reports ([#4167](https://github.com/letta-ai/letta-code/pull/4167), [#4152](https://github.com/letta-ai/letta-code/pull/4152))
- Removed the `letta cloud-mcp` command ([#4167](https://github.com/letta-ai/letta-code/pull/4167))

## 0.31.10

- Fixed the Task tool advertising its computer parameter on non-Cloud backends ([#4177](https://github.com/letta-ai/letta-code/pull/4177))

## 0.31.9

- Added a computer parameter to the Agent tool for running subagents on connected computers ([#4170](https://github.com/letta-ai/letta-code/pull/4170))
- Fixed teleporting default conversations and resuming the source conversation after a failed teleport handoff ([#4160](https://github.com/letta-ai/letta-code/pull/4160), [#4164](https://github.com/letta-ai/letta-code/pull/4164))
- Fixed headless environment-routed turns dropping the client tool allowlist and timing out after 10 minutes (turns now wait on environment liveness) ([#4171](https://github.com/letta-ai/letta-code/pull/4171), [#4172](https://github.com/letta-ai/letta-code/pull/4172), [#4174](https://github.com/letta-ai/letta-code/pull/4174))

## 0.31.8

- Added a unified `letta mcp` CLI with an agent tool search command, a built-in browser-use skill, and an exported default memory constraints policy ([#4151](https://github.com/letta-ai/letta-code/pull/4151), [#4155](https://github.com/letta-ai/letta-code/pull/4155), [#4137](https://github.com/letta-ai/letta-code/pull/4137), [#4140](https://github.com/letta-ai/letta-code/pull/4140))
- Changed subagent launches to always run in the background ([#4138](https://github.com/letta-ai/letta-code/pull/4138))
- Fixed permission allow-rule matching for commands with trailing `&&` or `||`, memory token estimates missing MemFS v2 core files, model overrides on forked subagents, and completed ChatGPT OAuth sessions not persisting ([#4131](https://github.com/letta-ai/letta-code/pull/4131), [#4147](https://github.com/letta-ai/letta-code/pull/4147), [#4154](https://github.com/letta-ai/letta-code/pull/4154), [#4048](https://github.com/letta-ai/letta-code/pull/4048))

## 0.31.7

- Fixed agent secrets retrieval to use the dedicated endpoint and routed all docs.letta.com reads through the letta-guide skill ([#4132](https://github.com/letta-ai/letta-code/pull/4132), [#4128](https://github.com/letta-ai/letta-code/pull/4128))

## 0.31.6

- Added automatic pushing of committed shared memory changes, agent-submitted user feedback, and enforcement of configurable memory limits ([#4103](https://github.com/letta-ai/letta-code/pull/4103), [#4104](https://github.com/letta-ai/letta-code/pull/4104), [#4105](https://github.com/letta-ai/letta-code/pull/4105))
- Removed the unused `dream` CLI subcommand ([#4092](https://github.com/letta-ai/letta-code/pull/4092))
- Fixed shared memory frontmatter validation, reflection retries for invalid models, and best-effort tool bootstrap failures leaking into headless output ([#4102](https://github.com/letta-ai/letta-code/pull/4102), [#4101](https://github.com/letta-ai/letta-code/pull/4101), [#4088](https://github.com/letta-ai/letta-code/pull/4088))
- Improved model provider compatibility by upgrading pi-ai to 0.84.4 and removing the temporary OpenRouter thinking-level patch ([#4108](https://github.com/letta-ai/letta-code/pull/4108))

## 0.31.5

- Fixed incomplete root-layout memory prompts ([#4093](https://github.com/letta-ai/letta-code/pull/4093))

## 0.31.4

- Added a configurable memory layout and agent-origin attribution for headless session telemetry ([#4085](https://github.com/letta-ai/letta-code/pull/4085), [#4082](https://github.com/letta-ai/letta-code/pull/4082))
- Fixed ChatGPT OAuth reasoning effort not persisting ([#4064](https://github.com/letta-ai/letta-code/pull/4064))

## 0.31.3

- Renamed `letta server-mcp` to `letta cloud-mcp` ([#4074](https://github.com/letta-ai/letta-code/pull/4074))
- Fixed the using-server-mcp skill being shown to local agents, and corrected the self-configuration, messaging-agents, finding-agents, and desktop preferences skills ([#4073](https://github.com/letta-ai/letta-code/pull/4073), [#4068](https://github.com/letta-ai/letta-code/pull/4068), [#4069](https://github.com/letta-ai/letta-code/pull/4069), [#4067](https://github.com/letta-ai/letta-code/pull/4067), [#4066](https://github.com/letta-ai/letta-code/pull/4066))

## 0.31.2

- Added the `letta server-mcp` CLI and a skill for agent-connected MCP servers ([#4047](https://github.com/letta-ai/letta-code/pull/4047))
- Fixed PowerShell command hooks not preserving native exit codes ([#4007](https://github.com/letta-ai/letta-code/pull/4007))

## 0.31.1

- Fixed runtime support for scoped managed workloads ([#4062](https://github.com/letta-ai/letta-code/pull/4062))

## 0.31.0

- Added pause and resume commands for scheduled tasks, a scheduled skill staleness watcher, and cloud-agent classification for OpenRouter traffic in local mode ([#4051](https://github.com/letta-ai/letta-code/pull/4051), [#4060](https://github.com/letta-ai/letta-code/pull/4060), [#3978](https://github.com/letta-ai/letta-code/pull/3978))
- Fixed the reasoning picker not appearing for local ChatGPT OAuth, the Tutor profile asset failing to load, channel lifecycle hooks blocking delivery queues, and repeated environment reminders in the listener ([#4026](https://github.com/letta-ai/letta-code/pull/4026), [#4031](https://github.com/letta-ai/letta-code/pull/4031), [#4044](https://github.com/letta-ai/letta-code/pull/4044), [#4059](https://github.com/letta-ai/letta-code/pull/4059))
- Fixed nested skills not using their frontmatter names and tightened memory-sync, dispatch model catalog, and MemFS repair guidance in bundled skills ([#4057](https://github.com/letta-ai/letta-code/pull/4057), [#4053](https://github.com/letta-ai/letta-code/pull/4053), [#4054](https://github.com/letta-ai/letta-code/pull/4054), [#4055](https://github.com/letta-ai/letta-code/pull/4055))
- Improved message routing for channel chats without threads ([#4027](https://github.com/letta-ai/letta-code/pull/4027))

## 0.30.32

- Added OpenRouter provider support with API key and OAuth sign-in, agent-free conversation runtimes in the app server, and a `letta secret` CLI subcommand for managing secrets ([#3979](https://github.com/letta-ai/letta-code/pull/3979), [#3878](https://github.com/letta-ai/letta-code/pull/3878), [#4023](https://github.com/letta-ai/letta-code/pull/4023))
- Fixed replay of recovered approval requests, memory commands running before MemFS sync completes, Ctrl-C interrupts in non-TTY sessions, Telegram chat ID validation, restored source file size checks, and silent stream recovery now being surfaced ([#4014](https://github.com/letta-ai/letta-code/pull/4014), [#4010](https://github.com/letta-ai/letta-code/pull/4010), [#4020](https://github.com/letta-ai/letta-code/pull/4020), [#4001](https://github.com/letta-ai/letta-code/pull/4001), [#4021](https://github.com/letta-ai/letta-code/pull/4021), [#4024](https://github.com/letta-ai/letta-code/pull/4024))
- Improved secret usage guidance in reminders and model provider compatibility by upgrading pi-ai to 0.84.3 ([#4019](https://github.com/letta-ai/letta-code/pull/4019), [#4011](https://github.com/letta-ai/letta-code/pull/4011))

## 0.30.31

- Fixed injected skill context messages leaking into the conversation view, mandatory reasoning metadata on local OpenRouter connections, and mod registry updates now batched during lifecycle events ([#4000](https://github.com/letta-ai/letta-code/pull/4000), [#4012](https://github.com/letta-ai/letta-code/pull/4012), [#3964](https://github.com/letta-ai/letta-code/pull/3964))

## 0.30.30

- Fixed client context restored after compaction, custom compaction prompts kept during the automatic full-summarization fallback, duplicate MemFS upstream configuration, and ChatGPT quota errors preserved so plan rotation can trigger ([#3974](https://github.com/letta-ai/letta-code/pull/3974), [#3977](https://github.com/letta-ai/letta-code/pull/3977), [#3984](https://github.com/letta-ai/letta-code/pull/3984), [#3990](https://github.com/letta-ai/letta-code/pull/3990))
- Fixed approval state only published while an approval is pending, approval classification outcome reporting, provider-aware toolset selection, bundled skill resources exposed on activation, and recovery when a completed turn loses its terminal stream events ([#3983](https://github.com/letta-ai/letta-code/pull/3983), [#3985](https://github.com/letta-ai/letta-code/pull/3985), [#3981](https://github.com/letta-ai/letta-code/pull/3981), [#3992](https://github.com/letta-ai/letta-code/pull/3992), [#3982](https://github.com/letta-ai/letta-code/pull/3982))
- Fixed interrupts stopping TaskOutput waits and cancelling remaining blocking work, and clarified Bash tool working-directory semantics ([#3995](https://github.com/letta-ai/letta-code/pull/3995), [#3996](https://github.com/letta-ai/letta-code/pull/3996), [#3994](https://github.com/letta-ai/letta-code/pull/3994))

## 0.30.29

- Added loading skills from attached shared memory ([#3965](https://github.com/letta-ai/letta-code/pull/3965))
- Fixed duplicate Telegram terminal notices, recovery of unrouted Discord threads, memory refresh before reflection integration, approval boundary state publishing, and image processing on Linux Desktop ([#3958](https://github.com/letta-ai/letta-code/pull/3958), [#3959](https://github.com/letta-ai/letta-code/pull/3959), [#3961](https://github.com/letta-ai/letta-code/pull/3961), [#3962](https://github.com/letta-ai/letta-code/pull/3962), [#3967](https://github.com/letta-ai/letta-code/pull/3967))
- Improved model provider compatibility by upgrading pi-ai to 0.84.2 ([#3903](https://github.com/letta-ai/letta-code/pull/3903))

## 0.30.28

- Added Grok subscription OAuth sign-in in local mode ([#3942](https://github.com/letta-ai/letta-code/pull/3942))
- Fixed secret injection for braced `${NAME}` shell references, resuming tasks after teleport, queue snapshot broadcasts when removing a missing item, exact run-to-send correlations, and runtime status re-emitted at turn boundaries ([#3920](https://github.com/letta-ai/letta-code/pull/3920), [#3939](https://github.com/letta-ai/letta-code/pull/3939), [#3923](https://github.com/letta-ai/letta-code/pull/3923), [#3904](https://github.com/letta-ai/letta-code/pull/3904), [#3924](https://github.com/letta-ai/letta-code/pull/3924))
- Improved system prompt wording to reduce repetition ([#3938](https://github.com/letta-ai/letta-code/pull/3938))

## 0.30.27

- Added automatic rotation to the next ChatGPT plan when quota is exhausted mid-turn ([#3911](https://github.com/letta-ai/letta-code/pull/3911))
- Fixed `apply_patch` rejecting duplicate resolved paths and headless runs following turns across task notifications ([#3916](https://github.com/letta-ai/letta-code/pull/3916), [#3917](https://github.com/letta-ai/letta-code/pull/3917))

## 0.30.26

- Added teleporting conversations to Desktop Local ([#3899](https://github.com/letta-ai/letta-code/pull/3899))
- Added shared Slack attachment handling and Telegram channel primitives for external channel hosts ([#3890](https://github.com/letta-ai/letta-code/pull/3890), [#3889](https://github.com/letta-ai/letta-code/pull/3889))
- Fixed remapping unsupported minimal reasoning effort for GPT-5.6, recovery of turns whose message stream dies silently mid-run, removal of models dropped from the hosted catalog, and the `xhigh` tier labeled Extra High when the catalog has a max tier ([#3877](https://github.com/letta-ai/letta-code/pull/3877), [#3882](https://github.com/letta-ai/letta-code/pull/3882), [#3887](https://github.com/letta-ai/letta-code/pull/3887), [#3896](https://github.com/letta-ai/letta-code/pull/3896))
- Fixed approvals distinguishing dropped tool arguments from model omissions, subagent-created PRs appearing on parent conversations, and isolation of channel startup failures on restore ([#3886](https://github.com/letta-ai/letta-code/pull/3886), [#3891](https://github.com/letta-ai/letta-code/pull/3891), [#3908](https://github.com/letta-ai/letta-code/pull/3908))

## 0.30.25

- Improved skill loading performance by avoiding request-time filesystem scans ([#3872](https://github.com/letta-ai/letta-code/pull/3872))
- Fixed headless ephemeral tools derived from the conversation model, contained background output write failures, and split-socket pairing across listener reconnects ([#3871](https://github.com/letta-ai/letta-code/pull/3871), [#3873](https://github.com/letta-ai/letta-code/pull/3873), [#3880](https://github.com/letta-ai/letta-code/pull/3880))

## 0.30.24

- Added agent-free ephemeral conversations in headless mode and a `SetWorkingDirectory` tool for changing the working directory between shell commands ([#3817](https://github.com/letta-ai/letta-code/pull/3817), [#3868](https://github.com/letta-ai/letta-code/pull/3868))
- Fixed queued sender attribution on continuations and restored queued delivery metadata ([#3866](https://github.com/letta-ai/letta-code/pull/3866), [#3869](https://github.com/letta-ai/letta-code/pull/3869))

## 0.30.23

- Added an official container image and proactive monitoring behavior for long-running work ([#3855](https://github.com/letta-ai/letta-code/pull/3855), [#3858](https://github.com/letta-ai/letta-code/pull/3858))
- Fixed teleport continuation retries to be idempotent ([#3865](https://github.com/letta-ai/letta-code/pull/3865))

## 0.30.22

- Added in-place working directory updates for running sessions and safe gateway handoff when teleporting channel conversations ([#3847](https://github.com/letta-ai/letta-code/pull/3847), [#3846](https://github.com/letta-ai/letta-code/pull/3846))
- Fixed preserving image results from external tools, tracking PRs created after heredocs, secret redaction scoped to each tool invocation, and retrying safe Cloud API shutdown rejections ([#3848](https://github.com/letta-ai/letta-code/pull/3848), [#3851](https://github.com/letta-ai/letta-code/pull/3851), [#3849](https://github.com/letta-ai/letta-code/pull/3849), [#3852](https://github.com/letta-ai/letta-code/pull/3852))

## 0.30.21

- Added runtime workspace sandboxes in the app server and mod-driven conversation title refreshes in the active TUI ([#3827](https://github.com/letta-ai/letta-code/pull/3827), [#3837](https://github.com/letta-ai/letta-code/pull/3837))
- Fixed TUI provider validation against supplied base URLs, Slack user mentions preserved in prompts, headless `can_use_tool` deny interrupts, and Ollama reporting its served context window instead of the GGUF maximum ([#3812](https://github.com/letta-ai/letta-code/pull/3812), [#3832](https://github.com/letta-ai/letta-code/pull/3832), [#3592](https://github.com/letta-ai/letta-code/pull/3592), [#3838](https://github.com/letta-ai/letta-code/pull/3838))
- Removed repeated delivery reminders and minimized post-send confirmations in channels ([#3834](https://github.com/letta-ai/letta-code/pull/3834), [#3835](https://github.com/letta-ai/letta-code/pull/3835))

## 0.30.20

- Added teleporting conversations between environments, with a skill guiding teleport workflows ([#3813](https://github.com/letta-ai/letta-code/pull/3813), [#3814](https://github.com/letta-ai/letta-code/pull/3814))
- Improved CLI startup time by lazily initializing the syntax highlighter ([#3824](https://github.com/letta-ai/letta-code/pull/3824))
- Fixed environment response correlation in headless mode, project settings loaded for sandbox transfers, output limits preserved when resuming agents, and mod-provided model providers during reflection ([#3805](https://github.com/letta-ai/letta-code/pull/3805), [#3809](https://github.com/letta-ai/letta-code/pull/3809), [#3810](https://github.com/letta-ai/letta-code/pull/3810), [#3815](https://github.com/letta-ai/letta-code/pull/3815))
- Fixed the Read tool’s line-number prefix matching Claude Code, `TaskUpdate` aligned with Anthropic’s schema, stale LS/MultiEdit/`TodoWrite` tools dropped from built-in subagents, subagent forks inheriting the parent toolset, and proactive Slack thread continuity ([#3816](https://github.com/letta-ai/letta-code/pull/3816), [#3819](https://github.com/letta-ai/letta-code/pull/3819), [#3823](https://github.com/letta-ai/letta-code/pull/3823), [#3826](https://github.com/letta-ai/letta-code/pull/3826), [#3820](https://github.com/letta-ai/letta-code/pull/3820))

## 0.30.19

- Added sandbox file transfer commands to the CLI ([#3800](https://github.com/letta-ai/letta-code/pull/3800))
- Fixed headless runs targeting the conversation’s cloud sandbox and typing indicators staying active across queued channel turns ([#3801](https://github.com/letta-ai/letta-code/pull/3801), [#3786](https://github.com/letta-ai/letta-code/pull/3786))
- Improved Bash and BashOutput tool descriptions to route long-running monitoring to the Monitor tool ([#3785](https://github.com/letta-ai/letta-code/pull/3785))

## 0.30.18

- No notable user-facing changes in this release

## 0.30.17

- Added shared Slack ingress and model picker primitives for external channel hosts ([#3776](https://github.com/letta-ai/letta-code/pull/3776))

## 0.30.16

- Fixed worktree path normalization on Windows, preserved Monitor output truncation markers, and approval-first turn input ordering in mods ([#3764](https://github.com/letta-ai/letta-code/pull/3764), [#3765](https://github.com/letta-ai/letta-code/pull/3765), [#3774](https://github.com/letta-ai/letta-code/pull/3774))

## 0.30.15

- Added hot-reloading of agent records from disk in local mode ([#3760](https://github.com/letta-ai/letta-code/pull/3760))
- Fixed sender attribution on live user echoes, empty Monitor source placeholders, API key validation against the supplied base URL when connecting providers, and unexpected git fetch prompts from worktrees ([#3755](https://github.com/letta-ai/letta-code/pull/3755), [#3756](https://github.com/letta-ai/letta-code/pull/3756), [#3716](https://github.com/letta-ai/letta-code/pull/3716), [#3761](https://github.com/letta-ai/letta-code/pull/3761))

## 0.30.14

- Added an `ExitWorktree` tool for leaving or cleaning up a worktree, with compact result summaries in the CLI, and event monitors ([#3747](https://github.com/letta-ai/letta-code/pull/3747), [#3752](https://github.com/letta-ai/letta-code/pull/3752), [#3751](https://github.com/letta-ai/letta-code/pull/3751))
- Added shared Slack reaction ingress policy and MessageChannel result classification for external channel hosts ([#3753](https://github.com/letta-ai/letta-code/pull/3753), [#3754](https://github.com/letta-ai/letta-code/pull/3754))

## 0.30.13

- Added GitHub PR tracking on conversations ([#3746](https://github.com/letta-ai/letta-code/pull/3746))
- Fixed general-purpose subagents inheriting the parent model, acting-user attribution on direct turns, and task notifications delivered when a background Bash command exits ([#3743](https://github.com/letta-ai/letta-code/pull/3743), [#3742](https://github.com/letta-ai/letta-code/pull/3742), [#3741](https://github.com/letta-ai/letta-code/pull/3741))

## 0.30.12

- Added user-only mod notifications surfaced in Desktop ([#3713](https://github.com/letta-ai/letta-code/pull/3713))
- Added a shared runtime-command executor and host-extra command definitions for external channel hosts ([#3733](https://github.com/letta-ai/letta-code/pull/3733), [#3740](https://github.com/letta-ai/letta-code/pull/3740))
- Fixed toolset details leaking into model updates, injected skill messages streaming live, recovered AskUserQuestion approvals re-presented after restart, root agent instructions loaded in worktrees, and manual toolsets scoped to conversations ([#3735](https://github.com/letta-ai/letta-code/pull/3735), [#3734](https://github.com/letta-ai/letta-code/pull/3734), [#3738](https://github.com/letta-ai/letta-code/pull/3738), [#3736](https://github.com/letta-ai/letta-code/pull/3736), [#3739](https://github.com/letta-ai/letta-code/pull/3739))

## 0.30.11

- Changed scheduled conversations to be tagged instead of prefixed in the title ([#3731](https://github.com/letta-ai/letta-code/pull/3731))
- Added lifecycle-error formatting and the slash-command surface for external channel hosts ([#3726](https://github.com/letta-ai/letta-code/pull/3726), [#3729](https://github.com/letta-ai/letta-code/pull/3729))
- Fixed duplicate outbound channel actions, environment skills registered in agent context, and channel-created conversations pinned to the agent’s current model ([#3704](https://github.com/letta-ai/letta-code/pull/3704), [#3728](https://github.com/letta-ai/letta-code/pull/3728), [#3732](https://github.com/letta-ai/letta-code/pull/3732))

## 0.30.10

- Added support for skill directories provided by the connected environment ([#3722](https://github.com/letta-ai/letta-code/pull/3722))
- Fixed loading bundled client tools named in the allowlist ([#3721](https://github.com/letta-ai/letta-code/pull/3721))

## 0.30.9

- Changed channel-created conversations to use conversation tags instead of source prefixes ([#3708](https://github.com/letta-ai/letta-code/pull/3708))
- Removed the experimental Responses WebSocket flag ([#3568](https://github.com/letta-ai/letta-code/pull/3568))
- Fixed model refresh after turn-start mods and the first provider retry now being shown ([#3702](https://github.com/letta-ai/letta-code/pull/3702), [#3706](https://github.com/letta-ai/letta-code/pull/3706))
- Fixed force-killing timed-out shell process trees, split stream socket liveness, direct turns staying on the process transport, and aborting wedged HTTP reads after a terminal SSE sequence ([#3714](https://github.com/letta-ai/letta-code/pull/3714), [#3718](https://github.com/letta-ai/letta-code/pull/3718), [#3717](https://github.com/letta-ai/letta-code/pull/3717), [#3720](https://github.com/letta-ai/letta-code/pull/3720))

## 0.30.8

- Changed conversation title generation to use Luna ([#3701](https://github.com/letta-ai/letta-code/pull/3701))
- Fixed headless retries of dropped streams on the active run, provider-aware auto toolsets, batched gateway runtime tool registration, channels waiting for the final turn lifecycle event, canonical notification envelopes, and preserved terminal error details ([#3694](https://github.com/letta-ai/letta-code/pull/3694), [#3698](https://github.com/letta-ai/letta-code/pull/3698), [#3693](https://github.com/letta-ai/letta-code/pull/3693), [#3696](https://github.com/letta-ai/letta-code/pull/3696), [#3700](https://github.com/letta-ai/letta-code/pull/3700), [#3699](https://github.com/letta-ai/letta-code/pull/3699))

## 0.30.7

- Fixed tool lifecycle events to preserve real message IDs ([#3685](https://github.com/letta-ai/letta-code/pull/3685))

## 0.30.6

- Added per-channel Slack mention gating so the agent only responds when mentioned in configured channels ([#3658](https://github.com/letta-ai/letta-code/pull/3658))
- Changed cron mechanics guidance to live in the scheduling-tasks skill ([#3683](https://github.com/letta-ai/letta-code/pull/3683))
- Fixed the self-hosted registration override, OpenAI-compatible providers on the local backend, cron preserving active listener execution, and cron falling back to a local schedule when Cloud can’t reach the computer ([#3663](https://github.com/letta-ai/letta-code/pull/3663), [#3674](https://github.com/letta-ai/letta-code/pull/3674), [#3665](https://github.com/letta-ai/letta-code/pull/3665), [#3682](https://github.com/letta-ai/letta-code/pull/3682))
- Fixed agent MemFS access in mod callbacks, reflection child processes isolated from mods, external tools bridged on remote connections, MemFS resetting inherited credential helpers, and terminal turn errors forwarded and sanitized ([#3673](https://github.com/letta-ai/letta-code/pull/3673), [#3676](https://github.com/letta-ai/letta-code/pull/3676), [#3679](https://github.com/letta-ai/letta-code/pull/3679), [#3670](https://github.com/letta-ai/letta-code/pull/3670), [#3678](https://github.com/letta-ai/letta-code/pull/3678), [#3680](https://github.com/letta-ai/letta-code/pull/3680))

## 0.30.5

- Added stateless sessions with existing agents and a `letta shared-memory` CLI subcommand with a git-first shared memory skill ([#3664](https://github.com/letta-ai/letta-code/pull/3664), [#3653](https://github.com/letta-ai/letta-code/pull/3653))
- Fixed `xhigh` reasoning tiers for the new Opus and Sonnet models, preserving the local backend after login, queued notification identity, and distinguishing switches to existing worktrees ([#3545](https://github.com/letta-ai/letta-code/pull/3545), [#3648](https://github.com/letta-ai/letta-code/pull/3648), [#3629](https://github.com/letta-ai/letta-code/pull/3629), [#3571](https://github.com/letta-ai/letta-code/pull/3571))
- Improved the reflection worktree integration flow ([#3534](https://github.com/letta-ai/letta-code/pull/3534))

## 0.30.4

- Added WhatsApp messaging controls and lifecycle hardening, stateful Responses chaining in the app server, and base64 encoding for the `read_file` device command ([#3650](https://github.com/letta-ai/letta-code/pull/3650), [#3639](https://github.com/letta-ai/letta-code/pull/3639), [#3649](https://github.com/letta-ai/letta-code/pull/3649))
- Fixed OAuth provider identity in the model selector and app-server tool execution without a relay connection ([#3651](https://github.com/letta-ai/letta-code/pull/3651), [#3654](https://github.com/letta-ai/letta-code/pull/3654))

## 0.30.3

- No notable user-facing changes in this release

## 0.30.2

- Fixed schedule listing to never silently omit Cloud schedules, and added a remove alias and name-based addressing for schedules ([#3623](https://github.com/letta-ai/letta-code/pull/3623))
- Fixed honoring managed runtime device identity ([#3624](https://github.com/letta-ai/letta-code/pull/3624))

## 0.30.1

- Added a shared scheduled-task prompt contract ([#3621](https://github.com/letta-ai/letta-code/pull/3621))

## 0.30.0

- Added request-scoped client toolsets in the Agent SDK ([#3609](https://github.com/letta-ai/letta-code/pull/3609))
- Fixed package manager shim launching on Windows, unavailable memory block counts omitted, stalled split-stream reconnect recovery, and headless mode rejecting implicit positional prompts ([#3600](https://github.com/letta-ai/letta-code/pull/3600), [#3607](https://github.com/letta-ai/letta-code/pull/3607), [#3598](https://github.com/letta-ai/letta-code/pull/3598), [#3611](https://github.com/letta-ai/letta-code/pull/3611))

## 0.29.13

- Added metadata-only overrides for subagents and surfaced server-side MCP servers in `/mcp` ([#3556](https://github.com/letta-ai/letta-code/pull/3556), [#3570](https://github.com/letta-ai/letta-code/pull/3570))
- Improved WhatsApp identity handling by canonicalizing LID identities ([#3599](https://github.com/letta-ai/letta-code/pull/3599))
- Fixed Fast OAuth provider identity preservation, concurrent local git config changes on the memory repo, and reflection prompts on Windows shells ([#3561](https://github.com/letta-ai/letta-code/pull/3561), [#3563](https://github.com/letta-ai/letta-code/pull/3563), [#3566](https://github.com/letta-ai/letta-code/pull/3566))

## 0.29.12

- Added Claude Opus 5 model support and per-agent client-side MCP servers with OAuth ([#3550](https://github.com/letta-ai/letta-code/pull/3550), [#3549](https://github.com/letta-ai/letta-code/pull/3549))
- Fixed shared channel reload command routing, repeated bot thread context in Slack, oversized persisted channel reminders, the Slack loading message limit, and reusable MCP client declarations ([#3528](https://github.com/letta-ai/letta-code/pull/3528), [#3551](https://github.com/letta-ai/letta-code/pull/3551), [#3552](https://github.com/letta-ai/letta-code/pull/3552), [#3553](https://github.com/letta-ai/letta-code/pull/3553), [#3557](https://github.com/letta-ai/letta-code/pull/3557))

## 0.29.11

- Fixed automatic titles for empty specified conversations, in-flight turns lost across relay reconnects, and false pong timeouts under event-loop stalls ([#3542](https://github.com/letta-ai/letta-code/pull/3542), [#3522](https://github.com/letta-ai/letta-code/pull/3522), [#3547](https://github.com/letta-ai/letta-code/pull/3547))

## 0.29.10

- Added shared cloud agents to the agent list, a built-in shared-memory management skill for cloud agents, and OpenAI Responses API support in the app server ([#3537](https://github.com/letta-ai/letta-code/pull/3537), [#3299](https://github.com/letta-ai/letta-code/pull/3299), [#3538](https://github.com/letta-ai/letta-code/pull/3538))

## 0.29.9

- Added a strict permissions mode that forces all tools through approval ([#3533](https://github.com/letta-ai/letta-code/pull/3533))

## 0.29.8

- Fixed shared memory prompt guidance so it only applies to hosted agents ([#3531](https://github.com/letta-ai/letta-code/pull/3531))

## 0.29.7

- Added support for concurrent app-server WebSocket clients ([#3524](https://github.com/letta-ai/letta-code/pull/3524))
- Fixed terminal startup to probe for an existing shell instead of assuming `/bin/zsh` ([#3529](https://github.com/letta-ai/letta-code/pull/3529))

## 0.29.6

- Added explicit Discord bot handoffs and a confinement launcher for memory workers ([#3426](https://github.com/letta-ai/letta-code/pull/3426), [#3525](https://github.com/letta-ai/letta-code/pull/3525))
- Fixed Telegram private bot topics and missing pagination metadata from `conversation_messages_list` ([#3211](https://github.com/letta-ai/letta-code/pull/3211), [#3526](https://github.com/letta-ai/letta-code/pull/3526))

## 0.29.5

- Fixed in-flight mod reload registrations and selectors not refreshing after mod provider registration ([#3501](https://github.com/letta-ai/letta-code/pull/3501), [#3503](https://github.com/letta-ai/letta-code/pull/3503))

## 0.29.4

- Fixed default Ollama context windows now capped at 128K, authenticated native websocket origins in the app server, AppleDouble agent sidecar files on macOS, compaction not triggering before output headroom is exhausted, and inconsistent endpoint context defaults ([#3512](https://github.com/letta-ai/letta-code/pull/3512), [#3511](https://github.com/letta-ai/letta-code/pull/3511), [#3514](https://github.com/letta-ai/letta-code/pull/3514), [#3516](https://github.com/letta-ai/letta-code/pull/3516), [#3513](https://github.com/letta-ai/letta-code/pull/3513))

## 0.29.3

- Fixed the app-server client contract so external clients can consume it ([#3502](https://github.com/letta-ai/letta-code/pull/3502))

## 0.29.2

- Added external client capability discovery to the app server ([#3500](https://github.com/letta-ai/letta-code/pull/3500))
- Fixed on-demand llama.cpp router models not appearing in local mode and fenced remote interrupt cancellation ([#3496](https://github.com/letta-ai/letta-code/pull/3496), [#3495](https://github.com/letta-ai/letta-code/pull/3495))

## 0.29.1

- Fixed OAuth flows not being registered in the standalone CLI bundle ([#3492](https://github.com/letta-ai/letta-code/pull/3492))

## 0.29.0

- Added BYOK OpenAI reasoning controls and responsive markdown table rendering in the CLI ([#3484](https://github.com/letta-ai/letta-code/pull/3484), [#3487](https://github.com/letta-ai/letta-code/pull/3487))
- Improved app-server protocol clients to inherit harness tool defaults, agents passing secrets into the programs they run, and skill dispatch guidance ([#3479](https://github.com/letta-ai/letta-code/pull/3479), [#3483](https://github.com/letta-ai/letta-code/pull/3483), [#3486](https://github.com/letta-ai/letta-code/pull/3486))
- Fixed adjacent reasoning headings rendering without separation ([#3485](https://github.com/letta-ai/letta-code/pull/3485))

## 0.28.18

- Added review of historical coding-agent sessions via @letta-ai/trajectory and surfaced OpenRouter reasoning effort levels ([#3459](https://github.com/letta-ai/letta-code/pull/3459), [#3469](https://github.com/letta-ai/letta-code/pull/3469))
- Improved reflection transcript handling with centralized normalization ([#3467](https://github.com/letta-ai/letta-code/pull/3467))
- Fixed clamping total tool return size before it reaches the model and scrubbing secrets from overflow file content ([#3470](https://github.com/letta-ai/letta-code/pull/3470), [#3471](https://github.com/letta-ai/letta-code/pull/3471))

## 0.28.17

- Added an OpenAI-compatible API for the App Server behind `--openai-api` ([#3427](https://github.com/letta-ai/letta-code/pull/3427))
- Added a seeded Tutor profile picture and refreshed the curated model catalog from the cloud catalog endpoint ([#3458](https://github.com/letta-ai/letta-code/pull/3458), [#3390](https://github.com/letta-ai/letta-code/pull/3390))
- Fixed listener identity handling with a spawner-assigned identity hook, no spawner identity inheritance, and no duplicate standalone listeners ([#3453](https://github.com/letta-ai/letta-code/pull/3453), [#3462](https://github.com/letta-ai/letta-code/pull/3462), [#3460](https://github.com/letta-ai/letta-code/pull/3460))
- Fixed the base URL field for local endpoint providers and pointed users at `--backend local` for local-only connect providers ([#3456](https://github.com/letta-ai/letta-code/pull/3456), [#3457](https://github.com/letta-ai/letta-code/pull/3457))

## 0.28.16

- Added task-first Tutor guidance, active config inspection, and a dedicated Tutor human prompt ([#3442](https://github.com/letta-ai/letta-code/pull/3442), [#3375](https://github.com/letta-ai/letta-code/pull/3375))
- Removed Constellation terminology from the CLI ([#3431](https://github.com/letta-ai/letta-code/pull/3431))
- Fixed transient OAuth response handling, eager React resolution for mods in packaged runtimes, and isolation of image processing diagnostics ([#3425](https://github.com/letta-ai/letta-code/pull/3425), [#3439](https://github.com/letta-ai/letta-code/pull/3439), [#3434](https://github.com/letta-ai/letta-code/pull/3434))
- Fixed the denial reason shown when stale approvals auto-close ([#3444](https://github.com/letta-ai/letta-code/pull/3444))

## 0.28.15

- Added Gemini 3.6 Flash on cloud ([#3441](https://github.com/letta-ai/letta-code/pull/3441))
- Fixed actionable errors for transient channel failures, cron field value range validation, Slack channel reply block reuse, and search results in the resume picker ([#3443](https://github.com/letta-ai/letta-code/pull/3443), [#3233](https://github.com/letta-ai/letta-code/pull/3233), [#3445](https://github.com/letta-ai/letta-code/pull/3445), [#3413](https://github.com/letta-ai/letta-code/pull/3413))

## 0.28.14

- Changed `letta cron` to route through durable Cloud schedules by default ([#3407](https://github.com/letta-ai/letta-code/pull/3407))
- Renamed the cron `--target-device` flag to `--computer` and added pre-validation against non-targetable list entries ([#3432](https://github.com/letta-ai/letta-code/pull/3432), [#3428](https://github.com/letta-ai/letta-code/pull/3428))
- Added centralized sender access control, command tiers, and `/whoami` for channels ([#3430](https://github.com/letta-ai/letta-code/pull/3430))
- Added a bundled letta-guide skill for answering Letta product questions from live docs ([#3440](https://github.com/letta-ai/letta-code/pull/3440))
- Fixed the Slack model picker layout and hardened channel pairing code generation ([#3429](https://github.com/letta-ai/letta-code/pull/3429), [#3433](https://github.com/letta-ai/letta-code/pull/3433))

## 0.28.13

- Fixed resuming project sessions before pinned agents ([#3418](https://github.com/letta-ai/letta-code/pull/3418))

## 0.28.12

- Added a self-configuration skill ([#3401](https://github.com/letta-ai/letta-code/pull/3401))
- Changed the App Server entry point to the unified `letta server` command ([#3415](https://github.com/letta-ai/letta-code/pull/3415))
- Fixed rebuilding stale approval input on resync in headless mode, hiding generic tool activity from Slack status, and exposing cloud as the backend name ([#3403](https://github.com/letta-ai/letta-code/pull/3403), [#3408](https://github.com/letta-ai/letta-code/pull/3408), [#3416](https://github.com/letta-ai/letta-code/pull/3416))

## 0.28.11

- Fixed GPT-5.6 context windows with explicit 1M variants and stopped omitting the context window limit on model-bearing updates ([#3383](https://github.com/letta-ai/letta-code/pull/3383), [#3386](https://github.com/letta-ai/letta-code/pull/3386))
- Fixed Slack file downloads wedging turns on slow or stalled transfers, Kimi K3 reasoning controls, and subagent results lost to silent stdout truncation ([#3382](https://github.com/letta-ai/letta-code/pull/3382), [#3387](https://github.com/letta-ai/letta-code/pull/3387), [#3303](https://github.com/letta-ai/letta-code/pull/3303))

## 0.28.10

- Added Kimi K3 model presets ([#3384](https://github.com/letta-ai/letta-code/pull/3384))

## 0.28.9

- Added a feedback command for channels ([#3373](https://github.com/letta-ai/letta-code/pull/3373))
- Fixed preserving unresolved secret refs in channels, saving `base_url` for local providers, loading agent-scoped MemFS mods in listener sessions, honoring runtime skill sources in the App Server, and emitting the subagent `conversation_id` in state snapshots ([#3371](https://github.com/letta-ai/letta-code/pull/3371), [#3331](https://github.com/letta-ai/letta-code/pull/3331), [#3344](https://github.com/letta-ai/letta-code/pull/3344), [#3370](https://github.com/letta-ai/letta-code/pull/3370), [#3240](https://github.com/letta-ai/letta-code/pull/3240))

## 0.28.8

- Added back GPT-5.6 Luna ChatGPT OAuth and OAuth 2.1 support in the mcp-http skill helper ([#3349](https://github.com/letta-ai/letta-code/pull/3349), [#3368](https://github.com/letta-ai/letta-code/pull/3368))
- Removed skill invocation arguments ([#3365](https://github.com/letta-ai/letta-code/pull/3365))
- Fixed the context-limit reset message for uncatalogued models, included authoritative time in scheduled cron prompts, and allowed explicitly mentioned bots in Slack ([#3350](https://github.com/letta-ai/letta-code/pull/3350), [#3348](https://github.com/letta-ai/letta-code/pull/3348), [#3366](https://github.com/letta-ai/letta-code/pull/3366))

## 0.28.7

- Fixed repairing stale conversation working directories and preserving image policy across turn retries ([#3318](https://github.com/letta-ai/letta-code/pull/3318), [#3360](https://github.com/letta-ai/letta-code/pull/3360))

## 0.28.6

- Added tags to onboarding-created agents ([#3356](https://github.com/letta-ai/letta-code/pull/3356))
- Fixed preserving access to oversized Slack attachments ([#3345](https://github.com/letta-ai/letta-code/pull/3345))
- Fixed local-mode model handling: isolated per-conversation model token settings, preserved provider length stop reasons, and stopped treating output limits as context overflow ([#3353](https://github.com/letta-ai/letta-code/pull/3353), [#3354](https://github.com/letta-ai/letta-code/pull/3354), [#3355](https://github.com/letta-ai/letta-code/pull/3355))
- Fixed authoritative executing tool IDs on listener loop state, App Server websocket disconnect visibility, and send-boundary image normalization ([#3352](https://github.com/letta-ai/letta-code/pull/3352), [#3358](https://github.com/letta-ai/letta-code/pull/3358), [#3357](https://github.com/letta-ai/letta-code/pull/3357))

## 0.28.5

- Added `--prompt` and `--system` reflection overrides for dreaming ([#3313](https://github.com/letta-ai/letta-code/pull/3313))
- Fixed grouping contiguous reasoning blocks in local mode, updating the in-flight turn tool context when EnterWorktree switches the working directory in listener sessions, preserving OAuth credentials across listener reconnects, and routing web links to current surfaces ([#3327](https://github.com/letta-ai/letta-code/pull/3327), [#3339](https://github.com/letta-ai/letta-code/pull/3339), [#3341](https://github.com/letta-ai/letta-code/pull/3341), [#3328](https://github.com/letta-ai/letta-code/pull/3328))

## 0.28.4

- Added model presentation presets ([#3326](https://github.com/letta-ai/letta-code/pull/3326))
- Fixed local mode using the native model inventory with curated presets and stopped GPG-signing harness git commits in memory repos ([#3321](https://github.com/letta-ai/letta-code/pull/3321), [#3322](https://github.com/letta-ai/letta-code/pull/3322))

## 0.28.3

- Fixed preserving user message correlation IDs in local mode ([#3317](https://github.com/letta-ai/letta-code/pull/3317))

## 0.28.2

- Fixed local mode preserving canonical providers during model carryover, preventing one-token llama.cpp responses, and omitting the unavailable GPT-5.6 Luna OAuth model ([#3136](https://github.com/letta-ai/letta-code/pull/3136), [#3314](https://github.com/letta-ai/letta-code/pull/3314), [#3304](https://github.com/letta-ai/letta-code/pull/3304))

## 0.28.1

- Added a reflection model override for dreaming ([#3306](https://github.com/letta-ai/letta-code/pull/3306))
- Fixed Slack acknowledgements for long-running work ([#3307](https://github.com/letta-ai/letta-code/pull/3307))

## 0.28.0

- Added GPT-5.6 model support in local mode, GPT-5.6 ChatGPT OAuth presets, and an OpenAI-compatible provider connection ([#3294](https://github.com/letta-ai/letta-code/pull/3294), [#3297](https://github.com/letta-ai/letta-code/pull/3297), [#3283](https://github.com/letta-ai/letta-code/pull/3283))
- Improved Slack progress to ride the assistant status line with markdown replies and web footnotes ([#3279](https://github.com/letta-ai/letta-code/pull/3279))

## 0.27.30

- Added GPT-5.6 and Grok 4.5 model support, per-account Slack text progress mode, and memfs-less worker agents with explicit per-session memory scopes ([#3277](https://github.com/letta-ai/letta-code/pull/3277), [#3285](https://github.com/letta-ai/letta-code/pull/3285), [#3290](https://github.com/letta-ai/letta-code/pull/3290))
- Fixed Slack progress cards staying open on non-root replies, duplicate `markdown_text` in stopped streams, dead-stream rewrites reduced to a single terminal summary line, and attachments hydrated from thread broadcast messages ([#3272](https://github.com/letta-ai/letta-code/pull/3272), [#3275](https://github.com/letta-ai/letta-code/pull/3275), [#3276](https://github.com/letta-ai/letta-code/pull/3276), [#3281](https://github.com/letta-ai/letta-code/pull/3281))
- Fixed cancellation of in-flight headless turns on SIGINT, waiting for the final assistant response in environment-routed runs, and patch context mismatch diagnostics ([#2884](https://github.com/letta-ai/letta-code/pull/2884), [#3239](https://github.com/letta-ai/letta-code/pull/3239), [#3271](https://github.com/letta-ai/letta-code/pull/3271))

## 0.27.29

- Improved `letta dream --to` to skip creating a placeholder doc when nothing is learned and to write more concise, timeless AGENTS.md entries ([#3264](https://github.com/letta-ai/letta-code/pull/3264), [#3266](https://github.com/letta-ai/letta-code/pull/3266))
- Fixed tool error output leaking into progress row titles, orphaned Slack progress streams, and stale model availability across provider reconnects ([#3263](https://github.com/letta-ai/letta-code/pull/3263), [#3265](https://github.com/letta-ai/letta-code/pull/3265), [#3267](https://github.com/letta-ai/letta-code/pull/3267))
- Removed the experimental node integration; `x-letta-node` is now only enabled via the `LETTA_NODE` environment variable ([#3262](https://github.com/letta-ai/letta-code/pull/3262))

## 0.27.28

- Added `letta dream --to` for agentic AGENTS.md maintenance (synced into MemFS `system/` before reflecting) and `letta dream --from` for reflecting on external sources via an adapter framework ([#3245](https://github.com/letta-ai/letta-code/pull/3245), [#3249](https://github.com/letta-ai/letta-code/pull/3249), [#3251](https://github.com/letta-ai/letta-code/pull/3251))
- Added rich live Slack progress cards and local tool calls and returns in headless stream-json output ([#3029](https://github.com/letta-ai/letta-code/pull/3029), [#3242](https://github.com/letta-ai/letta-code/pull/3242))
- Changed the shell tool to require a `description` parameter across toolsets ([#3254](https://github.com/letta-ai/letta-code/pull/3254))
- Fixed Slack progress cards stuck on dead streams, inbound Slack attachments inlined as base64 images, bidirectional interrupts in headless mode, and Bash recovery from deleted working directories ([#2631](https://github.com/letta-ai/letta-code/pull/2631), [#3238](https://github.com/letta-ai/letta-code/pull/3238), [#3255](https://github.com/letta-ai/letta-code/pull/3255), [#3260](https://github.com/letta-ai/letta-code/pull/3260))

## 0.27.27

- Added the `letta dream` subcommand for non-interactive reflection ([#3212](https://github.com/letta-ai/letta-code/pull/3212))
- Fixed memory write/delete responses and `memory_updated` events firing before the MemFS push completed ([#3243](https://github.com/letta-ai/letta-code/pull/3243))

## 0.27.26

- Added environment routing for headless messages, Slack auto-subscription to threads the agent sends messages to, and isolation of reflection MemFS writes in worktrees ([#3073](https://github.com/letta-ai/letta-code/pull/3073), [#3125](https://github.com/letta-ai/letta-code/pull/3125), [#3229](https://github.com/letta-ai/letta-code/pull/3229))
- Fixed non-retryable LLM errors being retried ([#3230](https://github.com/letta-ai/letta-code/pull/3230))

## 0.27.25

- Added acting-user attribution when the listener creates or forks conversations ([#3224](https://github.com/letta-ai/letta-code/pull/3224))
- Fixed skill loading to enforce the `name` frontmatter field ([#3218](https://github.com/letta-ai/letta-code/pull/3218))

## 0.27.24

- Added Tutor as the default agent for brand-new accounts ([#3220](https://github.com/letta-ai/letta-code/pull/3220))
- Improved the featured model list to current-generation models and the built-in review prompt ([#3219](https://github.com/letta-ai/letta-code/pull/3219), [#3222](https://github.com/letta-ai/letta-code/pull/3222))
- Fixed MemFS sync after skill installs, media in Slack thread context, and manual memory commit guidance ([#2936](https://github.com/letta-ai/letta-code/pull/2936), [#3156](https://github.com/letta-ai/letta-code/pull/3156), [#3187](https://github.com/letta-ai/letta-code/pull/3187))

## 0.27.23

- Changed the product status row into a built-in product-status panel ([#3203](https://github.com/letta-ai/letta-code/pull/3203))
- Fixed the deprecated `--no-memfs` flag to be accepted as a hidden no-op for version compatibility ([#3213](https://github.com/letta-ai/letta-code/pull/3213))

## 0.27.22

- Changed the cross-agent shell sandbox to opt-in while keeping the memory-subagent sandbox on by default ([#3209](https://github.com/letta-ai/letta-code/pull/3209))
- Fixed channel lifecycle errors to include run IDs ([#3183](https://github.com/letta-ai/letta-code/pull/3183))

## 0.27.21

- Added `exec_command` descriptions, stable listener instance IDs when registering environments, image assets in `list_memory` responses, conversation summaries and `agentId` in mod contexts, and agent creation presets exported as `@letta-ai/letta-code/agent-presets` ([#3130](https://github.com/letta-ai/letta-code/pull/3130), [#3193](https://github.com/letta-ai/letta-code/pull/3193), [#3197](https://github.com/letta-ai/letta-code/pull/3197), [#3200](https://github.com/letta-ai/letta-code/pull/3200), [#3204](https://github.com/letta-ai/letta-code/pull/3204), [#3206](https://github.com/letta-ai/letta-code/pull/3206))
- Changed subagents to run in the background by default, made MemFS mandatory with all non-MemFS opt-outs removed, and switched statusline panels to `ModContext` ([#3161](https://github.com/letta-ai/letta-code/pull/3161), [#3189](https://github.com/letta-ai/letta-code/pull/3189), [#3202](https://github.com/letta-ai/letta-code/pull/3202))
- Removed built-in goal mode ([#2792](https://github.com/letta-ai/letta-code/pull/2792))
- Fixed validation of auto-approved tool arguments, discovered local models in the model selector’s recommended tab, local favorites and favorite-backed pins in pinned agents, ChatGPT OAuth provider typing for OpenAI Codex, mod permissions in the listener/desktop runtime, queued reflection launch gating, app-server approval control requests, and startup MemFS enablement ([#3160](https://github.com/letta-ai/letta-code/pull/3160), [#3175](https://github.com/letta-ai/letta-code/pull/3175), [#3176](https://github.com/letta-ai/letta-code/pull/3176), [#3182](https://github.com/letta-ai/letta-code/pull/3182), [#3184](https://github.com/letta-ai/letta-code/pull/3184), [#3185](https://github.com/letta-ai/letta-code/pull/3185), [#3191](https://github.com/letta-ai/letta-code/pull/3191), [#3196](https://github.com/letta-ai/letta-code/pull/3196), [#3199](https://github.com/letta-ai/letta-code/pull/3199), [#3205](https://github.com/letta-ai/letta-code/pull/3205))

## 0.27.20

- Added `llm_end` mod events for provider errors ([#3164](https://github.com/letta-ai/letta-code/pull/3164))
- Fixed reaping of half-open sockets on both listener transports ([#3143](https://github.com/letta-ai/letta-code/pull/3143))

## 0.27.19

- Added Claude Sonnet 5 as the new default Sonnet model, autodetection of local model endpoints, `~` and `$VAR` expansion in `file_path` for Read/Write/Edit, syncing of attached repositories, `turn_start` cancellation and tool arguments in `tool_end` mod events, local filesystem mod learning, experimental desktop artifact file tools, an app-server conversation list client helper, and OpenRouter app attribution headers ([#2833](https://github.com/letta-ai/letta-code/pull/2833), [#3123](https://github.com/letta-ai/letta-code/pull/3123), [#3142](https://github.com/letta-ai/letta-code/pull/3142), [#3144](https://github.com/letta-ai/letta-code/pull/3144), [#3146](https://github.com/letta-ai/letta-code/pull/3146), [#3148](https://github.com/letta-ai/letta-code/pull/3148), [#3149](https://github.com/letta-ai/letta-code/pull/3149), [#3154](https://github.com/letta-ai/letta-code/pull/3154), [#3157](https://github.com/letta-ai/letta-code/pull/3157), [#3158](https://github.com/letta-ai/letta-code/pull/3158))
- Improved cohesion across the system prompt, tool descriptions, and the cron reminder ([#2808](https://github.com/letta-ai/letta-code/pull/2808))
- Fixed dreaming link visibility in tmux, Discord thread creation to respect the `auto_thread_on_mention` setting, stale mod dependency cache symlinks, full context in panel renders, bare `exit` routing before queueing, omitted `multiSelect` in AskUserQuestion, canonical project skills in the Skill tool, boot-directory fallback when the persisted working directory is deleted, fork subagents linked to their forked conversation, system memory path guidance, and orphaned CLI processes exiting when the parent dies ([#3099](https://github.com/letta-ai/letta-code/pull/3099), [#3103](https://github.com/letta-ai/letta-code/pull/3103), [#3117](https://github.com/letta-ai/letta-code/pull/3117), [#3120](https://github.com/letta-ai/letta-code/pull/3120), [#3122](https://github.com/letta-ai/letta-code/pull/3122), [#3126](https://github.com/letta-ai/letta-code/pull/3126), [#3127](https://github.com/letta-ai/letta-code/pull/3127), [#3131](https://github.com/letta-ai/letta-code/pull/3131), [#3145](https://github.com/letta-ai/letta-code/pull/3145), [#3147](https://github.com/letta-ai/letta-code/pull/3147), [#3152](https://github.com/letta-ai/letta-code/pull/3152))

## 0.27.18

- Added `tool_end` mod events with result modification, local-backend `compact_start`/`compact_end` and `llm_start`/`llm_end` events, `tool_start`/`tool_end` delivery on desktop, a `turn_end` continue effect for the listener, render-function panels, `updateLlmConfig` on the mod conversation handle for model/reasoning/context window changes, and mod slash commands advertised to clients via `mod_commands` ([#3087](https://github.com/letta-ai/letta-code/pull/3087), [#3092](https://github.com/letta-ai/letta-code/pull/3092), [#3096](https://github.com/letta-ai/letta-code/pull/3096), [#3097](https://github.com/letta-ai/letta-code/pull/3097), [#3101](https://github.com/letta-ai/letta-code/pull/3101), [#3102](https://github.com/letta-ai/letta-code/pull/3102), [#3107](https://github.com/letta-ai/letta-code/pull/3107), [#3112](https://github.com/letta-ai/letta-code/pull/3112))
- Changed the statusline API to signed-order panels and removed the memory permission mode ([#3093](https://github.com/letta-ai/letta-code/pull/3093), [#3104](https://github.com/letta-ai/letta-code/pull/3104))
- Fixed panel renders decoupled from input keystroke churn, Discord typing indicators while turns process, wide-character and emoji-aware panel widths, and diagnostics for invalid panel renderers ([#3057](https://github.com/letta-ai/letta-code/pull/3057), [#3094](https://github.com/letta-ai/letta-code/pull/3094), [#3105](https://github.com/letta-ai/letta-code/pull/3105), [#3113](https://github.com/letta-ai/letta-code/pull/3113))

## 0.27.17

- Added a `turn_end` mod event with a continue effect across the CLI, headless mode, and the desktop listener, the `letta/glm` model preset, and a default-on kernel filesystem sandbox for cross-agent isolation ([#2853](https://github.com/letta-ai/letta-code/pull/2853), [#3070](https://github.com/letta-ai/letta-code/pull/3070), [#3077](https://github.com/letta-ai/letta-code/pull/3077), [#3080](https://github.com/letta-ai/letta-code/pull/3080), [#3082](https://github.com/letta-ai/letta-code/pull/3082))
- Improved the reflection prompt and exposed the Edit tool to the reflection agent ([#2789](https://github.com/letta-ai/letta-code/pull/2789), [#3088](https://github.com/letta-ai/letta-code/pull/3088))
- Fixed pinned-agent scoping and resuming a single existing pin, and ChatGPT Plus/Pro provider type inference on desktop ([#3081](https://github.com/letta-ai/letta-code/pull/3081), [#3083](https://github.com/letta-ai/letta-code/pull/3083))

## 0.27.16

- Added mod package management for npm, GitHub, and git packages, secrets exposed to mod tool invocations, a result effect on the `tool_start` mod event, and automatic provisioning, entry, and locking in CreateWorktree ([#3046](https://github.com/letta-ai/letta-code/pull/3046), [#3055](https://github.com/letta-ai/letta-code/pull/3055), [#3058](https://github.com/letta-ai/letta-code/pull/3058), [#3062](https://github.com/letta-ai/letta-code/pull/3062), [#3074](https://github.com/letta-ai/letta-code/pull/3074), [#3075](https://github.com/letta-ai/letta-code/pull/3075))
- Fixed desktop toolset refresh to use the selected provider ([#3067](https://github.com/letta-ai/letta-code/pull/3067))

## 0.27.15

- Added mod packages: scaffold, install (local and npm), manage, list, and validate mod packages, plus agent-scoped MemFS mods ([#3030](https://github.com/letta-ai/letta-code/pull/3030), [#3031](https://github.com/letta-ai/letta-code/pull/3031), [#3032](https://github.com/letta-ai/letta-code/pull/3032), [#3033](https://github.com/letta-ai/letta-code/pull/3033), [#3036](https://github.com/letta-ai/letta-code/pull/3036), [#3038](https://github.com/letta-ai/letta-code/pull/3038), [#3039](https://github.com/letta-ai/letta-code/pull/3039), [#3040](https://github.com/letta-ai/letta-code/pull/3040), [#3054](https://github.com/letta-ai/letta-code/pull/3054))
- Added manual multi-transcript reflection, ChatGPT OAuth provider aliases, local agent secret storage, and parent tags on subagents ([#2600](https://github.com/letta-ai/letta-code/pull/2600), [#2971](https://github.com/letta-ai/letta-code/pull/2971), [#3021](https://github.com/letta-ai/letta-code/pull/3021), [#3052](https://github.com/letta-ai/letta-code/pull/3052))
- Fixed hidden agents appearing in local listings, rehydrating bot-authored Slack thread context, keeping MessageChannel for scoped no-tool turns, retrying skipped auto-reflection launches, loading legacy extensions alongside mods, subagent prompt state over websocket, and preserving BYOK reasoning settings on desktop and in the TUI ([#2912](https://github.com/letta-ai/letta-code/pull/2912), [#2968](https://github.com/letta-ai/letta-code/pull/2968), [#3014](https://github.com/letta-ai/letta-code/pull/3014), [#3022](https://github.com/letta-ai/letta-code/pull/3022), [#3034](https://github.com/letta-ai/letta-code/pull/3034), [#3047](https://github.com/letta-ai/letta-code/pull/3047), [#3049](https://github.com/letta-ai/letta-code/pull/3049), [#3051](https://github.com/letta-ai/letta-code/pull/3051))

## 0.27.14

- Improved agent pins in settings ([#2951](https://github.com/letta-ai/letta-code/pull/2951))
- Fixed channel conversation working-directory mappings and stale approval loop status in the app server ([#2944](https://github.com/letta-ai/letta-code/pull/2944), [#3012](https://github.com/letta-ai/letta-code/pull/3012))

## 0.27.13

- Added a Codex-style websocket auth guard to the app server ([#3008](https://github.com/letta-ai/letta-code/pull/3008))

## 0.27.12

- Added a first-party Signal channel, Slack reaction and listen-mode controls, Kimi 2.7 model support, and the `turn_start` event for listener mods ([#2931](https://github.com/letta-ai/letta-code/pull/2931), [#2933](https://github.com/letta-ai/letta-code/pull/2933), [#2998](https://github.com/letta-ai/letta-code/pull/2998), [#3002](https://github.com/letta-ai/letta-code/pull/3002))
- Improved reflection task notifications with the reflection agent ID and warnings on UTF-8 memory writes ([#2956](https://github.com/letta-ai/letta-code/pull/2956), [#2980](https://github.com/letta-ai/letta-code/pull/2980))
- Fixed stale in-context messages on resume, forked conversations overwriting existing conversations, restored channel accounts scoped by backend, active-shell detection for startup notes, session tool filters applied to client snapshots, secrets reminders refreshing after changes, app-server `runTurn` approval terminality, and hidden console windows for git context on Windows ([#2960](https://github.com/letta-ai/letta-code/pull/2960), [#2962](https://github.com/letta-ai/letta-code/pull/2962), [#2965](https://github.com/letta-ai/letta-code/pull/2965), [#2967](https://github.com/letta-ai/letta-code/pull/2967), [#2972](https://github.com/letta-ai/letta-code/pull/2972), [#2991](https://github.com/letta-ai/letta-code/pull/2991), [#2999](https://github.com/letta-ai/letta-code/pull/2999), [#3006](https://github.com/letta-ai/letta-code/pull/3006))

## 0.27.11

- Added mod event propagation through listener tool-preparation paths and surfaced GLM 5.2 for zAI local connections ([#2949](https://github.com/letta-ai/letta-code/pull/2949), [#2957](https://github.com/letta-ai/letta-code/pull/2957))
- Fixed image tool-return validation for canonical image content, hardened desktop listener shutdown handling with explicit desktop-mode detection, and added a Windows path-length hint for worktree creation ([#2943](https://github.com/letta-ai/letta-code/pull/2943), [#2953](https://github.com/letta-ai/letta-code/pull/2953), [#2955](https://github.com/letta-ai/letta-code/pull/2955))

## 0.27.10

- Added GLM 5.2 model support, rich Telegram messages, inbound Slack audio transcription, and scoped mod invocation context ([#2940](https://github.com/letta-ai/letta-code/pull/2940), [#2901](https://github.com/letta-ai/letta-code/pull/2901), [#2924](https://github.com/letta-ai/letta-code/pull/2924), [#2861](https://github.com/letta-ai/letta-code/pull/2861))
- Fixed conversation carry-over context windows, scoped memory filesystem handling in websocket listener memory commands, local MemFS enablement, Slack DM/thread routing, direct skill file URLs, and local desktop conversation renames ([#2867](https://github.com/letta-ai/letta-code/pull/2867), [#2863](https://github.com/letta-ai/letta-code/pull/2863), [#2945](https://github.com/letta-ai/letta-code/pull/2945), [#2947](https://github.com/letta-ai/letta-code/pull/2947), [#2908](https://github.com/letta-ai/letta-code/pull/2908), [#2932](https://github.com/letta-ai/letta-code/pull/2932), [#2930](https://github.com/letta-ai/letta-code/pull/2930), [#2923](https://github.com/letta-ai/letta-code/pull/2923))
- Removed legacy sleeptime-agent, memory-block, skills-block migration, and block-label plumbing paths ([#2873](https://github.com/letta-ai/letta-code/pull/2873), [#2874](https://github.com/letta-ai/letta-code/pull/2874), [#2875](https://github.com/letta-ai/letta-code/pull/2875))

## 0.27.9

- Added the app-server protocol/client path, runtime-start tool callbacks, always-ask permissions, and always-ask mod policy ([#2813](https://github.com/letta-ai/letta-code/pull/2813), [#2828](https://github.com/letta-ai/letta-code/pull/2828), [#2830](https://github.com/letta-ai/letta-code/pull/2830), [#2832](https://github.com/letta-ai/letta-code/pull/2832), [#2834](https://github.com/letta-ai/letta-code/pull/2834), [#2843](https://github.com/letta-ai/letta-code/pull/2843), [#2844](https://github.com/letta-ai/letta-code/pull/2844), [#2846](https://github.com/letta-ai/letta-code/pull/2846), [#2860](https://github.com/letta-ai/letta-code/pull/2860), [#2852](https://github.com/letta-ai/letta-code/pull/2852), [#2849](https://github.com/letta-ai/letta-code/pull/2849))
- Renamed local extensions to mods and added a desktop customization skill ([#2798](https://github.com/letta-ai/letta-code/pull/2798), [#2803](https://github.com/letta-ai/letta-code/pull/2803))
- Fixed local/Fable model behavior, MemFS push reliability, active Slack thread replies, cron Send now, TUI overlay rendering, pending approval tool cleanup, and context estimation/oversized payload recovery in local mode ([#2806](https://github.com/letta-ai/letta-code/pull/2806), [#2809](https://github.com/letta-ai/letta-code/pull/2809), [#2811](https://github.com/letta-ai/letta-code/pull/2811), [#2819](https://github.com/letta-ai/letta-code/pull/2819), [#2820](https://github.com/letta-ai/letta-code/pull/2820), [#2838](https://github.com/letta-ai/letta-code/pull/2838), [#2851](https://github.com/letta-ai/letta-code/pull/2851), [#2821](https://github.com/letta-ai/letta-code/pull/2821), [#2823](https://github.com/letta-ai/letta-code/pull/2823), [#2824](https://github.com/letta-ai/letta-code/pull/2824), [#2842](https://github.com/letta-ai/letta-code/pull/2842))

## 0.27.8

- Added built-in image generation and Claude Fable 5 model support ([#2788](https://github.com/letta-ai/letta-code/pull/2788), [#2794](https://github.com/letta-ai/letta-code/pull/2794))
- Fixed agent import path traversal, explicit-repo worktree creation, bundled skill scripts, refreshed secret reminders, and feedback dialog sizing ([#2777](https://github.com/letta-ai/letta-code/pull/2777), [#2782](https://github.com/letta-ai/letta-code/pull/2782), [#2778](https://github.com/letta-ai/letta-code/pull/2778), [#2780](https://github.com/letta-ai/letta-code/pull/2780), [#2786](https://github.com/letta-ai/letta-code/pull/2786))

## 0.27.7

- Added vim-style `j`/`k` navigation to list selectors ([#2673](https://github.com/letta-ai/letta-code/pull/2673))
- Fixed saved backend preferences in subcommands, explicit cloud-agent startup, local pinned-agent startup, default MemFS enablement for new agents, local model token limits, updater execution on Windows, and ripgrep resolution ([#2772](https://github.com/letta-ai/letta-code/pull/2772), [#2750](https://github.com/letta-ai/letta-code/pull/2750), [#2763](https://github.com/letta-ai/letta-code/pull/2763), [#2755](https://github.com/letta-ai/letta-code/pull/2755), [#2767](https://github.com/letta-ai/letta-code/pull/2767), [#2765](https://github.com/letta-ai/letta-code/pull/2765), [#2769](https://github.com/letta-ai/letta-code/pull/2769))

## 0.27.6

- Added generated conversation titles and extension permission overlays ([#2721](https://github.com/letta-ai/letta-code/pull/2721), [#2752](https://github.com/letta-ai/letta-code/pull/2752))
- Fixed provider-field placeholders and markdown rendering in question prompts, and removed the experimental tool-start denial path ([#2748](https://github.com/letta-ai/letta-code/pull/2748), [#2757](https://github.com/letta-ai/letta-code/pull/2757), [#2754](https://github.com/letta-ai/letta-code/pull/2754))

## 0.27.5

- Expanded extension diagnostics, desktop provider loading, remote reload, and local provider docs ([#2727](https://github.com/letta-ai/letta-code/pull/2727), [#2732](https://github.com/letta-ai/letta-code/pull/2732), [#2734](https://github.com/letta-ai/letta-code/pull/2734), [#2735](https://github.com/letta-ai/letta-code/pull/2735), [#2743](https://github.com/letta-ai/letta-code/pull/2743), [#2736](https://github.com/letta-ai/letta-code/pull/2736), [#2746](https://github.com/letta-ai/letta-code/pull/2746))
- Centralized MemFS sync after turns and fixed local provider, startup, subagent, and unified exec edge cases ([#2677](https://github.com/letta-ai/letta-code/pull/2677), [#2740](https://github.com/letta-ai/letta-code/pull/2740), [#2720](https://github.com/letta-ai/letta-code/pull/2720), [#2744](https://github.com/letta-ai/letta-code/pull/2744), [#2747](https://github.com/letta-ai/letta-code/pull/2747), [#2742](https://github.com/letta-ai/letta-code/pull/2742), [#2737](https://github.com/letta-ai/letta-code/pull/2737))

## 0.27.4

- Added local connect-provider websocket/write commands, stream response-state IDs, and extension diagnostics files ([#2680](https://github.com/letta-ai/letta-code/pull/2680), [#2717](https://github.com/letta-ai/letta-code/pull/2717), [#2719](https://github.com/letta-ai/letta-code/pull/2719), [#2718](https://github.com/letta-ai/letta-code/pull/2718), [#2725](https://github.com/letta-ai/letta-code/pull/2725))
- Fixed Slack bot reaction echoes, runtime surface reload, Windows Bash wording, and shell placeholder flicker ([#2722](https://github.com/letta-ai/letta-code/pull/2722), [#2726](https://github.com/letta-ai/letta-code/pull/2726), [#2712](https://github.com/letta-ai/letta-code/pull/2712), [#2716](https://github.com/letta-ai/letta-code/pull/2716))

## 0.27.3

- Added version-managed system prompts ([#2686](https://github.com/letta-ai/letta-code/pull/2686))
- Fixed orphaned tool-call rendering, skill creator scripts under ESM, PowerShell background fallback, websocket reflection transcripts, extension setup flow, and automatic conversation-title defaults ([#2699](https://github.com/letta-ai/letta-code/pull/2699), [#2698](https://github.com/letta-ai/letta-code/pull/2698), [#2685](https://github.com/letta-ai/letta-code/pull/2685), [#2659](https://github.com/letta-ai/letta-code/pull/2659), [#2700](https://github.com/letta-ai/letta-code/pull/2700), [#2708](https://github.com/letta-ai/letta-code/pull/2708))

## 0.27.2

- Added a typed Letta Code upgrade command ([#2599](https://github.com/letta-ai/letta-code/pull/2599))
- Fixed Telegram account commands, kept the default conversation permanently pinned, and continued the extension adapter refactor ([#2693](https://github.com/letta-ai/letta-code/pull/2693), [#2687](https://github.com/letta-ai/letta-code/pull/2687), [#2688](https://github.com/letta-ai/letta-code/pull/2688), [#2689](https://github.com/letta-ai/letta-code/pull/2689), [#2691](https://github.com/letta-ai/letta-code/pull/2691), [#2692](https://github.com/letta-ai/letta-code/pull/2692), [#2695](https://github.com/letta-ai/letta-code/pull/2695))

## 0.27.1

- Replaced `TodoWrite` with the `Task*` CRUD tool family ([#1937](https://github.com/letta-ai/letta-code/pull/1937))
- Fixed subagent telemetry flushing, non-UTF-8 text mutations, and PowerShell launcher alignment ([#2678](https://github.com/letta-ai/letta-code/pull/2678), [#2681](https://github.com/letta-ai/letta-code/pull/2681), [#2682](https://github.com/letta-ai/letta-code/pull/2682))

## 0.27.0

- Added MiniMax M3 and shared conversation pins with resume-selector support ([#2665](https://github.com/letta-ai/letta-code/pull/2665), [#2624](https://github.com/letta-ai/letta-code/pull/2624), [#2626](https://github.com/letta-ai/letta-code/pull/2626))
- Made generated conversation titles a default setting and aligned Codex tool schema descriptions ([#2674](https://github.com/letta-ai/letta-code/pull/2674), [#2675](https://github.com/letta-ai/letta-code/pull/2675))

## 0.26.9

- Added slash command overrides, per-run cron conversations, immediate cron triggering, Codex-style terminal titles, and mid-conversation local memory updates for Opus 4.8 ([#2656](https://github.com/letta-ai/letta-code/pull/2656), [#2618](https://github.com/letta-ai/letta-code/pull/2618), [#2668](https://github.com/letta-ai/letta-code/pull/2668), [#2670](https://github.com/letta-ai/letta-code/pull/2670), [#2611](https://github.com/letta-ai/letta-code/pull/2611))
- Fixed slash command autocomplete density, local startup model discovery, headless memory-guard defaults, Tutor onboarding, Claude Code dispatch guidance, and tool-call transcript snapshots ([#2625](https://github.com/letta-ai/letta-code/pull/2625), [#2663](https://github.com/letta-ai/letta-code/pull/2663), [#2641](https://github.com/letta-ai/letta-code/pull/2641), [#2667](https://github.com/letta-ai/letta-code/pull/2667), [#2660](https://github.com/letta-ai/letta-code/pull/2660), [#2661](https://github.com/letta-ai/letta-code/pull/2661), [#2671](https://github.com/letta-ai/letta-code/pull/2671))

## 0.26.8

- Added cron run history and schedule outcome recording ([#2647](https://github.com/letta-ai/letta-code/pull/2647), [#2649](https://github.com/letta-ai/letta-code/pull/2649))
- Renamed extension internals from runtime/host to adapter/engine ([#2651](https://github.com/letta-ai/letta-code/pull/2651), [#2653](https://github.com/letta-ai/letta-code/pull/2653))

## 0.26.7

- Fixed missing agent-file failures, on-demand file autocomplete, filesystem command indexing, resume startup loading, and pinned local-agent selection ([#2629](https://github.com/letta-ai/letta-code/pull/2629), [#2633](https://github.com/letta-ai/letta-code/pull/2633), [#2634](https://github.com/letta-ai/letta-code/pull/2634), [#2635](https://github.com/letta-ai/letta-code/pull/2635), [#2636](https://github.com/letta-ai/letta-code/pull/2636), [#2637](https://github.com/letta-ai/letta-code/pull/2637), [#2638](https://github.com/letta-ai/letta-code/pull/2638))

## 0.26.6

- Added ChatGPT Fast selector support in local mode ([#2620](https://github.com/letta-ai/letta-code/pull/2620))
- Fixed provider disconnect management, Codex stdin polling cancellation, and one-shot command guidance ([#2619](https://github.com/letta-ai/letta-code/pull/2619), [#2627](https://github.com/letta-ai/letta-code/pull/2627), [#2628](https://github.com/letta-ai/letta-code/pull/2628))

## 0.26.5

- Added an extension startup disable switch ([#2610](https://github.com/letta-ai/letta-code/pull/2610))
- Fixed local transcript recall, forced device status replay, TUI diff tab rendering, pending approval resume detection, local ChatGPT OAuth toolsets, and dreaming-agent links in tmux ([#2613](https://github.com/letta-ai/letta-code/pull/2613), [#2615](https://github.com/letta-ai/letta-code/pull/2615), [#2607](https://github.com/letta-ai/letta-code/pull/2607), [#2566](https://github.com/letta-ai/letta-code/pull/2566), [#2608](https://github.com/letta-ai/letta-code/pull/2608), [#2602](https://github.com/letta-ai/letta-code/pull/2602))

## 0.26.4

- Added hook input rewrites, Claude Opus 4.8, local OAuth/extension provider support, v2 local session transcripts, skill management commands, and telemetry segmentation ([#2518](https://github.com/letta-ai/letta-code/pull/2518), [#2584](https://github.com/letta-ai/letta-code/pull/2584), [#2587](https://github.com/letta-ai/letta-code/pull/2587), [#2590](https://github.com/letta-ai/letta-code/pull/2590), [#2585](https://github.com/letta-ai/letta-code/pull/2585), [#2588](https://github.com/letta-ai/letta-code/pull/2588), [#2568](https://github.com/letta-ai/letta-code/pull/2568))
- Fixed stale credential reauth, local default-conversation rename rejection, model context-window reporting, lazy transcript startup, provider registry replacement, and bootstrap relevance calibration ([#2592](https://github.com/letta-ai/letta-code/pull/2592), [#2580](https://github.com/letta-ai/letta-code/pull/2580), [#2575](https://github.com/letta-ai/letta-code/pull/2575), [#2582](https://github.com/letta-ai/letta-code/pull/2582), [#2589](https://github.com/letta-ai/letta-code/pull/2589), [#2581](https://github.com/letta-ai/letta-code/pull/2581))

## 0.26.3

- Added extension backend primitives, lifecycle events, headless extension tools, conversation-history access, secure channel credential storage, and quiet hook output ([#2538](https://github.com/letta-ai/letta-code/pull/2538), [#2542](https://github.com/letta-ai/letta-code/pull/2542), [#2544](https://github.com/letta-ai/letta-code/pull/2544), [#2546](https://github.com/letta-ai/letta-code/pull/2546), [#2547](https://github.com/letta-ai/letta-code/pull/2547), [#2556](https://github.com/letta-ai/letta-code/pull/2556), [#2548](https://github.com/letta-ai/letta-code/pull/2548), [#2514](https://github.com/letta-ai/letta-code/pull/2514))
- Fixed live scheduled task messages in Desktop, listener busy-run handling, no-op memory write errors, channel lifecycle errors, local model overrides, Desktop tutorial agent creation, and Slack account display names ([#2418](https://github.com/letta-ai/letta-code/pull/2418), [#2427](https://github.com/letta-ai/letta-code/pull/2427), [#2540](https://github.com/letta-ai/letta-code/pull/2540), [#2467](https://github.com/letta-ai/letta-code/pull/2467), [#2549](https://github.com/letta-ai/letta-code/pull/2549), [#2570](https://github.com/letta-ai/letta-code/pull/2570), [#2574](https://github.com/letta-ai/letta-code/pull/2574))

## 0.26.2

- Added the statusline renderer/runtime/setup flow and extension slash commands/tools ([#2482](https://github.com/letta-ai/letta-code/pull/2482), [#2500](https://github.com/letta-ai/letta-code/pull/2500), [#2501](https://github.com/letta-ai/letta-code/pull/2501), [#2502](https://github.com/letta-ai/letta-code/pull/2502), [#2504](https://github.com/letta-ai/letta-code/pull/2504), [#2506](https://github.com/letta-ai/letta-code/pull/2506), [#2519](https://github.com/letta-ai/letta-code/pull/2519), [#2524](https://github.com/letta-ai/letta-code/pull/2524), [#2526](https://github.com/letta-ai/letta-code/pull/2526))
- Added the WhatsApp channel, Tutor personality, Telegram topic/mention routing, channel `/model` command, and local-backend channel listener support ([#2102](https://github.com/letta-ai/letta-code/pull/2102), [#2479](https://github.com/letta-ai/letta-code/pull/2479), [#2463](https://github.com/letta-ai/letta-code/pull/2463))
- Fixed local/provider and startup polish around explicit target fallback, default conversation timestamps, local transcripts, LM Studio/Ollama Cloud, MCP overlay loading, context-limit preservation, memory clone timeouts, cron parsing, and agent selector rendering ([#2480](https://github.com/letta-ai/letta-code/pull/2480), [#2483](https://github.com/letta-ai/letta-code/pull/2483), [#2484](https://github.com/letta-ai/letta-code/pull/2484), [#2485](https://github.com/letta-ai/letta-code/pull/2485), [#2492](https://github.com/letta-ai/letta-code/pull/2492), [#2513](https://github.com/letta-ai/letta-code/pull/2513), [#2458](https://github.com/letta-ai/letta-code/pull/2458), [#2522](https://github.com/letta-ai/letta-code/pull/2522), [#2508](https://github.com/letta-ai/letta-code/pull/2508), [#2496](https://github.com/letta-ai/letta-code/pull/2496), [#2507](https://github.com/letta-ai/letta-code/pull/2507), [#2491](https://github.com/letta-ai/letta-code/pull/2491))

## 0.26.1

- Improved local-first startup polish: skipped cloud recents while logged out, preserved no-model placeholders, added rotating empty-composer hints, and added a login action to the Constellation empty state ([#2466](https://github.com/letta-ai/letta-code/pull/2466), [#2465](https://github.com/letta-ai/letta-code/pull/2465), [#2470](https://github.com/letta-ai/letta-code/pull/2470), [#2469](https://github.com/letta-ai/letta-code/pull/2469), [#2472](https://github.com/letta-ai/letta-code/pull/2472))
- Fixed Constellation login/connect flows by keeping OAuth polling alive across rerenders and allowing Esc to cancel OAuth overlays ([#2471](https://github.com/letta-ai/letta-code/pull/2471), [#2474](https://github.com/letta-ai/letta-code/pull/2474))
- Fixed startup routing for explicit agent targets and removed a pinned-tab fallback that could show the wrong recent agents ([#2477](https://github.com/letta-ai/letta-code/pull/2477), [#2476](https://github.com/letta-ai/letta-code/pull/2476))

## 0.26.0

- Added the local-first setup flow, first-turn bootstrap, local/Constellation agent tabs, backend toggle in the new-agent flow, and clearer startup hints for fresh local sessions ([#2339](https://github.com/letta-ai/letta-code/pull/2339), [#2403](https://github.com/letta-ai/letta-code/pull/2403), [#2419](https://github.com/letta-ai/letta-code/pull/2419), [#2452](https://github.com/letta-ai/letta-code/pull/2452), [#2436](https://github.com/letta-ai/letta-code/pull/2436), [#2438](https://github.com/letta-ai/letta-code/pull/2438), [#2441](https://github.com/letta-ai/letta-code/pull/2441), [#2442](https://github.com/letta-ai/letta-code/pull/2442), [#2450](https://github.com/letta-ai/letta-code/pull/2450))
- Removed plan mode, renamed the max-context command to `/context-limit`, and replaced memory-scope permission controls with the parent-process memory guard opt-out ([#2413](https://github.com/letta-ai/letta-code/pull/2413), [#2409](https://github.com/letta-ai/letta-code/pull/2409), [#2423](https://github.com/letta-ai/letta-code/pull/2423))
- Added channel slash commands, fixed Discord open-channel routing, hid stuck approval conflicts, and relaxed reflection error details outside debug mode ([#2405](https://github.com/letta-ai/letta-code/pull/2405), [#2386](https://github.com/letta-ai/letta-code/pull/2386), [#2379](https://github.com/letta-ai/letta-code/pull/2379), [#2412](https://github.com/letta-ai/letta-code/pull/2412))
- Added conversation cwd-map protocol support, sent run IDs with feedback, added Gemini 3.5 Flash, and made Bun the lockfile source of truth ([#2433](https://github.com/letta-ai/letta-code/pull/2433), [#2420](https://github.com/letta-ai/letta-code/pull/2420), [#2356](https://github.com/letta-ai/letta-code/pull/2356), [#2448](https://github.com/letta-ai/letta-code/pull/2448))
- Improved backend-aware session resume, local memory commits, OAuth token refresh, credit-limit messages, and remote environment registration retries ([#2434](https://github.com/letta-ai/letta-code/pull/2434), [#2340](https://github.com/letta-ai/letta-code/pull/2340), [#2351](https://github.com/letta-ai/letta-code/pull/2351), [#2391](https://github.com/letta-ai/letta-code/pull/2391), [#2372](https://github.com/letta-ai/letta-code/pull/2372))

## 0.25.11

- Added schema-driven custom channels, consolidated Discord per-channel policy work, and clarified channel opt-out envelopes and lifecycle error text ([#2210](https://github.com/letta-ai/letta-code/pull/2210), [#2329](https://github.com/letta-ai/letta-code/pull/2329), [#2332](https://github.com/letta-ai/letta-code/pull/2332), [#2313](https://github.com/letta-ai/letta-code/pull/2313))
- Added the first-class worktree creation tool, model-selector recents, terminal window title configuration, Ctrl+O shell output expansion, and Ctrl+D queue defer mode ([#1942](https://github.com/letta-ai/letta-code/pull/1942), [#2291](https://github.com/letta-ai/letta-code/pull/2291), [#2333](https://github.com/letta-ai/letta-code/pull/2333), [#2305](https://github.com/letta-ai/letta-code/pull/2305), [#2338](https://github.com/letta-ai/letta-code/pull/2338))
- Added the New tab to the agent browser and migrated several selectors to the shared overlay picker system ([#2337](https://github.com/letta-ai/letta-code/pull/2337), [#2343](https://github.com/letta-ai/letta-code/pull/2343), [#2341](https://github.com/letta-ai/letta-code/pull/2341), [#2346](https://github.com/letta-ai/letta-code/pull/2346), [#2349](https://github.com/letta-ai/letta-code/pull/2349), [#2375](https://github.com/letta-ai/letta-code/pull/2375), [#2377](https://github.com/letta-ai/letta-code/pull/2377))
- Tightened repository structure with named exports, layer-boundary checks, colocated tests, kebab-case TypeScript filenames, absolute imports, no circular dependencies, and export-function declarations ([#2354](https://github.com/letta-ai/letta-code/pull/2354), [#2359](https://github.com/letta-ai/letta-code/pull/2359), [#2361](https://github.com/letta-ai/letta-code/pull/2361), [#2374](https://github.com/letta-ai/letta-code/pull/2374), [#2355](https://github.com/letta-ai/letta-code/pull/2355), [#2362](https://github.com/letta-ai/letta-code/pull/2362), [#2363](https://github.com/letta-ai/letta-code/pull/2363), [#2364](https://github.com/letta-ai/letta-code/pull/2364), [#2370](https://github.com/letta-ai/letta-code/pull/2370))
- Fixed local transcript migrations, local subagent model inheritance, retryable run metadata, quota messages, memory git auth redaction, and transient provider retries ([#2302](https://github.com/letta-ai/letta-code/pull/2302), [#2310](https://github.com/letta-ai/letta-code/pull/2310), [#2315](https://github.com/letta-ai/letta-code/pull/2315), [#2303](https://github.com/letta-ai/letta-code/pull/2303), [#2348](https://github.com/letta-ai/letta-code/pull/2348), [#2320](https://github.com/letta-ai/letta-code/pull/2320))

## 0.25.10

- Fixed local transcript manifest repair, routed MemFS UI through local-backend paths, refreshed secrets before local secret commands, and added OpenCode-style provider timeouts ([#2295](https://github.com/letta-ai/letta-code/pull/2295), [#2282](https://github.com/letta-ai/letta-code/pull/2282), [#2292](https://github.com/letta-ai/letta-code/pull/2292), [#2251](https://github.com/letta-ai/letta-code/pull/2251))
- Improved provider stream disconnect messaging, nullable turn payload handling, reasoning whitespace, and Telegram block quote rendering ([#2276](https://github.com/letta-ai/letta-code/pull/2276), [#2293](https://github.com/letta-ai/letta-code/pull/2293), [#2278](https://github.com/letta-ai/letta-code/pull/2278), [#2296](https://github.com/letta-ai/letta-code/pull/2296))
- Simplified queue editing so Up-arrow loads all queued content ([#2288](https://github.com/letta-ai/letta-code/pull/2288))

## 0.25.9

- Added memory-focused subagent tool scoping, onboarding memory for Linus and Kawaii agents, the Blank personality, and guidance for agent config context in skills ([#2248](https://github.com/letta-ai/letta-code/pull/2248), [#2247](https://github.com/letta-ai/letta-code/pull/2247), [#2181](https://github.com/letta-ai/letta-code/pull/2181), [#2254](https://github.com/letta-ai/letta-code/pull/2254))
- Added a permissions startup note, backfilled skipped startup notes, moved reflection transcript paths to environment variables, and made large subagent prompt transport more robust ([#2249](https://github.com/letta-ai/letta-code/pull/2249), [#2250](https://github.com/letta-ai/letta-code/pull/2250), [#2253](https://github.com/letta-ai/letta-code/pull/2253), [#2265](https://github.com/letta-ai/letta-code/pull/2265))
- Added `/reload`, channel `/help`, remote compact command support, local max-context carry-over, and the shadow TUI cron experiment ([#2274](https://github.com/letta-ai/letta-code/pull/2274), [#2266](https://github.com/letta-ai/letta-code/pull/2266), [#2238](https://github.com/letta-ai/letta-code/pull/2238), [#2257](https://github.com/letta-ai/letta-code/pull/2257), [#2262](https://github.com/letta-ai/letta-code/pull/2262))
- Fixed forwarded Slack message retention, long highlighted user-message wrapping, and current Bun text-loader syntax ([#2263](https://github.com/letta-ai/letta-code/pull/2263), [#2268](https://github.com/letta-ai/letta-code/pull/2268), [#2261](https://github.com/letta-ai/letta-code/pull/2261))

## 0.25.8

- Renamed permission modes for clarity and made unrestricted the default ([#2197](https://github.com/letta-ai/letta-code/pull/2197))
- Added `/goal` for long-running autonomous objectives and refined channel pairing, interactive question prompts, Discord default permission modes, and `MessageChannel` reply contract reminders ([#2177](https://github.com/letta-ai/letta-code/pull/2177), [#2195](https://github.com/letta-ai/letta-code/pull/2195), [#2193](https://github.com/letta-ai/letta-code/pull/2193), [#2194](https://github.com/letta-ai/letta-code/pull/2194), [#2231](https://github.com/letta-ai/letta-code/pull/2231))
- Improved CLI rendering for status lines, prompt bullets, tool-call headers, file/search summaries, Read display, and shell/list/search labels ([#2199](https://github.com/letta-ai/letta-code/pull/2199), [#2209](https://github.com/letta-ai/letta-code/pull/2209), [#2219](https://github.com/letta-ai/letta-code/pull/2219), [#2225](https://github.com/letta-ai/letta-code/pull/2225), [#2222](https://github.com/letta-ai/letta-code/pull/2222), [#2240](https://github.com/letta-ai/letta-code/pull/2240))
- Fixed local interrupted-tool recovery and backfill projection, Slack list-marker formatting, and deferred tool-call commit handling ([#2211](https://github.com/letta-ai/letta-code/pull/2211), [#2230](https://github.com/letta-ai/letta-code/pull/2230), [#2229](https://github.com/letta-ai/letta-code/pull/2229), [#2206](https://github.com/letta-ai/letta-code/pull/2206), [#2236](https://github.com/letta-ai/letta-code/pull/2236))

## 0.25.7

- Restricted file tools available to memory subagents to keep them scoped to memory operations ([#2189](https://github.com/letta-ai/letta-code/pull/2189))
- Guarded tool-call terminal states in the TUI and aligned local-backend compaction formatting with the API ([#2188](https://github.com/letta-ai/letta-code/pull/2188), [#2190](https://github.com/letta-ai/letta-code/pull/2190))

## 0.25.6

- Refactored the CLI App layout and added wiring tests that auto-discover interactive app source files ([#2166](https://github.com/letta-ai/letta-code/pull/2166), [#2175](https://github.com/letta-ai/letta-code/pull/2175))
- Added markdown code block syntax highlighting and rendered retry events as status lines in the TUI ([#2186](https://github.com/letta-ai/letta-code/pull/2186), [#2187](https://github.com/letta-ai/letta-code/pull/2187))
- Added update aliases to the CLI and shared the terminal theme cache in the bundled CLI ([#2174](https://github.com/letta-ai/letta-code/pull/2174), [#2176](https://github.com/letta-ai/letta-code/pull/2176))
- Fixed local-backend compaction on overflow/usage triggers, transient provider stream retries, and tool backfill preservation on local resume ([#2178](https://github.com/letta-ai/letta-code/pull/2178), [#2179](https://github.com/letta-ai/letta-code/pull/2179), [#2183](https://github.com/letta-ai/letta-code/pull/2183))
- Notified chats when channel turns fail ([#2101](https://github.com/letta-ai/letta-code/pull/2101))

## 0.25.5

- Added slash invocation for skills and showed all skill source tabs in the `/skills` dialog ([#2157](https://github.com/letta-ai/letta-code/pull/2157), [#2159](https://github.com/letta-ai/letta-code/pull/2159))
- Improved Telegram channel response routing and deduped Discord ingress by message id ([#2151](https://github.com/letta-ai/letta-code/pull/2151), [#2081](https://github.com/letta-ai/letta-code/pull/2081))
- Routed local-backend commands, message search, and image paste paths through the backend abstraction; added websocket-listener support for the local backend ([#2158](https://github.com/letta-ai/letta-code/pull/2158), [#2160](https://github.com/letta-ai/letta-code/pull/2160), [#2161](https://github.com/letta-ai/letta-code/pull/2161), [#2171](https://github.com/letta-ai/letta-code/pull/2171))
- Added local sliding-window compaction, no-MemFS local sessions, and image-history modality guards ([#2169](https://github.com/letta-ai/letta-code/pull/2169), [#2170](https://github.com/letta-ai/letta-code/pull/2170), [#2164](https://github.com/letta-ai/letta-code/pull/2164))
- Propagated backend mode to subagents and removed the `blocks` CLI subcommand ([#2167](https://github.com/letta-ai/letta-code/pull/2167), [#2163](https://github.com/letta-ai/letta-code/pull/2163))
- Fixed bash preview prompt spacing, user-highlight vertical padding, and listener pong lifecycle parsing ([#2168](https://github.com/letta-ai/letta-code/pull/2168), [#2162](https://github.com/letta-ai/letta-code/pull/2162), [#2099](https://github.com/letta-ai/letta-code/pull/2099))

## 0.25.4

- Added the `ci-failure-detector` agent skill ([#2150](https://github.com/letta-ai/letta-code/pull/2150))
- Fixed local-backend ChatGPT OAuth requests and normalized `llm_error` stream stop reasons ([#2149](https://github.com/letta-ai/letta-code/pull/2149), [#2124](https://github.com/letta-ai/letta-code/pull/2124))

## 0.25.3

- Added a `--local` CLI flag and enabled provider connections for the new local backend ([#2126](https://github.com/letta-ai/letta-code/pull/2126), [#2147](https://github.com/letta-ai/letta-code/pull/2147))
- Wrapped `/btw` in approval recovery and retried transient OpenRouter errors ([#2133](https://github.com/letta-ai/letta-code/pull/2133), [#2108](https://github.com/letta-ai/letta-code/pull/2108))
- Enabled the automated PR reviewer for all authors ([#2145](https://github.com/letta-ai/letta-code/pull/2145))

## 0.25.2

- Added client-side conversation titles with opt-in AI title generation ([#2122](https://github.com/letta-ai/letta-code/pull/2122))
- Added Amelia as an automated PR code reviewer with refined prompts and stock-phrase outcomes ([#2127](https://github.com/letta-ai/letta-code/pull/2127), [#2135](https://github.com/letta-ai/letta-code/pull/2135), [#2139](https://github.com/letta-ai/letta-code/pull/2139))
- Auto-enabled MemFS for existing agents in headless mode and repaired malformed memory remotes ([#2128](https://github.com/letta-ai/letta-code/pull/2128), [#2138](https://github.com/letta-ai/letta-code/pull/2138))
- Showed Cloudflare transient errors instead of a generic LLM API error and gated post-stop approval recovery ([#2136](https://github.com/letta-ai/letta-code/pull/2136), [#2103](https://github.com/letta-ai/letta-code/pull/2103))
- Synced the Codex system prompt to GPT-5.5 ([#2141](https://github.com/letta-ai/letta-code/pull/2141))

## 0.25.1

- Added local MemFS support and local compaction ([#2076](https://github.com/letta-ai/letta-code/pull/2076), [#2106](https://github.com/letta-ai/letta-code/pull/2106))
- Added websocket commands for deleting memory files and split-channel repair on current main ([#2098](https://github.com/letta-ai/letta-code/pull/2098), [#2096](https://github.com/letta-ai/letta-code/pull/2096))
- Improved permission denial messages for memory-mode and expanded the memory git allowlist ([#2107](https://github.com/letta-ai/letta-code/pull/2107), [#2093](https://github.com/letta-ai/letta-code/pull/2093), [#2089](https://github.com/letta-ai/letta-code/pull/2089))
- Fixed reflection subagent MemFS cwd, validation of missing tool args before permissions, and `/btw` on default conversation ([#2083](https://github.com/letta-ai/letta-code/pull/2083), [#2090](https://github.com/letta-ai/letta-code/pull/2090), [#2121](https://github.com/letta-ai/letta-code/pull/2121))
- Unblocked memory-mode subagents on commit flows ([#2092](https://github.com/letta-ai/letta-code/pull/2092))

## 0.25.0

- Aligned the Letta system prompt with the Context Constitution ([#2040](https://github.com/letta-ai/letta-code/pull/2040))
- Added the `set-max-context` CLI command ([#2082](https://github.com/letta-ai/letta-code/pull/2082))
- Introduced the local-backend foundation: API backend seam, local backend implementation, and local MemFS system-prompt compilation ([#2064](https://github.com/letta-ai/letta-code/pull/2064), [#2065](https://github.com/letta-ai/letta-code/pull/2065), [#2066](https://github.com/letta-ai/letta-code/pull/2066))
- Hydrated local MemFS state from agent tags ([#2084](https://github.com/letta-ai/letta-code/pull/2084))
- Fixed streamed reasoning blocks to split on new OTID and avoided NBSP cursor placeholders in the TUI ([#2044](https://github.com/letta-ai/letta-code/pull/2044), [#2013](https://github.com/letta-ai/letta-code/pull/2013))
- Preserved Telegram photo MIME types on inbound messages ([#2050](https://github.com/letta-ai/letta-code/pull/2050))
- Improved listener performance via cached secrets hydration, cached client skills payload, preserved bootstrap reminders on reconnect, metadata reuse during tool prep, dedup image normalization, idle input fast-path, and post-sync state warming ([#2055](https://github.com/letta-ai/letta-code/pull/2055), [#2056](https://github.com/letta-ai/letta-code/pull/2056), [#2057](https://github.com/letta-ai/letta-code/pull/2057), [#2058](https://github.com/letta-ai/letta-code/pull/2058), [#2059](https://github.com/letta-ai/letta-code/pull/2059), [#2060](https://github.com/letta-ai/letta-code/pull/2060), [#2061](https://github.com/letta-ai/letta-code/pull/2061))

## 0.24.13

- Added dynamic channel plugin support ([#2021](https://github.com/letta-ai/letta-code/pull/2021))
- Added a websocket command for writing and syncing a memory file ([#2030](https://github.com/letta-ai/letta-code/pull/2030))
- Added secrets support in Letta Code Desktop and a `LETTA_DISABLE_CRON_SCHEDULER` opt-out ([#2046](https://github.com/letta-ai/letta-code/pull/2046), [#2047](https://github.com/letta-ai/letta-code/pull/2047))
- Skipped `.letta/worktrees` in @-mention and quick-pick file searches ([#2049](https://github.com/letta-ai/letta-code/pull/2049))
- Trimmed reflection launch context and clarified its system prompt ([#2031](https://github.com/letta-ai/letta-code/pull/2031))
- Added an API backend facade and routed headless lifecycle, stream-JSON controls, and headless tests through it ([#2034](https://github.com/letta-ai/letta-code/pull/2034), [#2035](https://github.com/letta-ai/letta-code/pull/2035), [#2036](https://github.com/letta-ai/letta-code/pull/2036), [#2037](https://github.com/letta-ai/letta-code/pull/2037))
- Fixed Kimi K2.6 output token handling ([#2042](https://github.com/letta-ai/letta-code/pull/2042))
- Fixed desktop listener registration with the local environment server when channels are enabled ([#2052](https://github.com/letta-ai/letta-code/pull/2052))

## 0.24.12

- Hardened Discord delivery error replies ([#2022](https://github.com/letta-ai/letta-code/pull/2022))
- Added a websocket override for `unsupported_1` ([#2024](https://github.com/letta-ai/letta-code/pull/2024))

## 0.24.11

- Added request-scoped client tool allowlists for listener mode ([#2016](https://github.com/letta-ai/letta-code/pull/2016))
- Moved WebSocket account configuration into channel plugin payloads ([#2015](https://github.com/letta-ai/letta-code/pull/2015))
- Centralized Letta API calls behind a single helper ([#2017](https://github.com/letta-ai/letta-code/pull/2017))
- Forwarded Discord delivery errors back to the originating user ([#2018](https://github.com/letta-ai/letta-code/pull/2018))
- Refreshed OTIDs for post-stop listener retries and honored reflection subagent model overrides ([#2020](https://github.com/letta-ai/letta-code/pull/2020), [#2014](https://github.com/letta-ai/letta-code/pull/2014))

## 0.24.10

- Added a runtime last-environment header for listener requests ([#2003](https://github.com/letta-ai/letta-code/pull/2003))
- Cached `messages.retrieve` to reduce redundant API calls ([#2006](https://github.com/letta-ai/letta-code/pull/2006))
- Injected shell secrets via environment variables and hydrated secrets for websocket shell tools ([#2007](https://github.com/letta-ai/letta-code/pull/2007), [#2002](https://github.com/letta-ai/letta-code/pull/2002))
- Stripped ANSI sequences from streaming shell tool output ([#2009](https://github.com/letta-ai/letta-code/pull/2009))
- Hardened WezTerm config injection to avoid corrupting commented configs ([#1941](https://github.com/letta-ai/letta-code/pull/1941), [#2012](https://github.com/letta-ai/letta-code/pull/2012))
- Skipped MemFS checkout when the remote has no HEAD ([#2005](https://github.com/letta-ai/letta-code/pull/2005))

## 0.24.9

- Added a Discord guild channel allowlist and fixed Discord direct-message routing ([#1950](https://github.com/letta-ai/letta-code/pull/1950), [#1944](https://github.com/letta-ai/letta-code/pull/1944))
- Supported local channel listeners on self-hosted servers ([#1993](https://github.com/letta-ai/letta-code/pull/1993))
- Removed GPT-5.5 Pro ([#2000](https://github.com/letta-ai/letta-code/pull/2000))

## 0.24.8

- Re-rooted the file index when the current working directory is a git worktree ([#1980](https://github.com/letta-ai/letta-code/pull/1980))
- Added runtime experiment toggles for Node ([#1986](https://github.com/letta-ai/letta-code/pull/1986))
- Improved startup performance by deduping subagent and headless `agents.retrieve` calls, caching agent state in the headless loop, skipping `syncAgentState` on tool-result continuations in bypass mode, and guarding init effects against double-fires ([#1988](https://github.com/letta-ai/letta-code/pull/1988), [#1981](https://github.com/letta-ai/letta-code/pull/1981), [#1983](https://github.com/letta-ai/letta-code/pull/1983), [#1987](https://github.com/letta-ai/letta-code/pull/1987), [#1989](https://github.com/letta-ai/letta-code/pull/1989), [#1990](https://github.com/letta-ai/letta-code/pull/1990))

## 0.24.7

- Added the `configuring-your-harness` built-in skill for deterministic harness configuration ([#1978](https://github.com/letta-ai/letta-code/pull/1978))
- Added websocket hot-reload of permission settings ([#1970](https://github.com/letta-ai/letta-code/pull/1970))
- Capped reflection (dream) startup context ([#1977](https://github.com/letta-ai/letta-code/pull/1977))
- Fixed headless terminal stream-JSON flushing ([#1975](https://github.com/letta-ai/letta-code/pull/1975))

## 0.24.6

- Routed desktop MemFS git transport transiently and refreshed memory git origin before write guards ([#1969](https://github.com/letta-ai/letta-code/pull/1969), [#1967](https://github.com/letta-ai/letta-code/pull/1967))
- Fixed authentication for the headless runner ([#1972](https://github.com/letta-ai/letta-code/pull/1972))

## 0.24.5

- Added the DeepSeek V4 Pro model ([#1961](https://github.com/letta-ai/letta-code/pull/1961))
- Used the CLI token estimator in prompts ([#1960](https://github.com/letta-ai/letta-code/pull/1960))
- Validated the MemFS sync endpoint on desktop enable and routed websocket git sync through the desktop proxy ([#1962](https://github.com/letta-ai/letta-code/pull/1962), [#1964](https://github.com/letta-ai/letta-code/pull/1964))
- Aliased Letta environment variables for PowerShell ([#1963](https://github.com/letta-ai/letta-code/pull/1963))

## 0.24.4

- Made sync approval recovery explicit in listener mode ([#1956](https://github.com/letta-ai/letta-code/pull/1956))

## 0.24.3

- Renamed the `letta memfs` CLI subcommand to `letta memory` ([#1955](https://github.com/letta-ai/letta-code/pull/1955))
- Added `letta memory tokens` for inspecting memory token usage ([#1939](https://github.com/letta-ai/letta-code/pull/1939))
- Added websocket emit telemetry, protocol telemetry to file, and local activity telemetry to file ([#1945](https://github.com/letta-ai/letta-code/pull/1945), [#1952](https://github.com/letta-ai/letta-code/pull/1952), [#1953](https://github.com/letta-ai/letta-code/pull/1953))
- Throttled streaming tool output and surfaced approval-continuation retries in the listener ([#1946](https://github.com/letta-ai/letta-code/pull/1946), [#1954](https://github.com/letta-ai/letta-code/pull/1954))

## 0.24.2

- Added GPT-5.5 ([#1947](https://github.com/letta-ai/letta-code/pull/1947))
- Added Kimi K2 BYOK ([#1938](https://github.com/letta-ai/letta-code/pull/1938))
- Flushed the final headless stdout chunk before exit ([#1943](https://github.com/letta-ai/letta-code/pull/1943))

## 0.24.1

- Added `should_doctor` device-status logic for `/doctor` triggers ([#1599](https://github.com/letta-ai/letta-code/pull/1599))
- Surfaced the Task tool as `Agent` for Claude Code parity ([#1911](https://github.com/letta-ai/letta-code/pull/1911))
- Supported a separate MemFS base URL via `LETTA_MEMFS_BASE_URL` and stopped blocking interactive startup on sync ([#1918](https://github.com/letta-ai/letta-code/pull/1918), [#1916](https://github.com/letta-ai/letta-code/pull/1916))
- Made `context_doctor` conservative about system-prompt edits ([#1921](https://github.com/letta-ai/letta-code/pull/1921))
- Routed Gemini models through the default toolset and hid legacy models without dropping their metadata ([#1924](https://github.com/letta-ai/letta-code/pull/1924), [#1923](https://github.com/letta-ai/letta-code/pull/1923))
- Hardened HEIC handling and image-resize behavior across shared image tools ([#1920](https://github.com/letta-ai/letta-code/pull/1920), [#1922](https://github.com/letta-ai/letta-code/pull/1922))
- Prevented MessageChannel from leaking into unrouted conversations and confined cwd switches to the conversation that created the worktree ([#1915](https://github.com/letta-ai/letta-code/pull/1915), [#1925](https://github.com/letta-ai/letta-code/pull/1925))

## 0.24.0

- Added the `modifying-letta-code` built-in skill ([#1887](https://github.com/letta-ai/letta-code/pull/1887))
- Added `/memory-repository` for pushing agent memory to an additional git remote ([#1899](https://github.com/letta-ai/letta-code/pull/1899))
- Always used `letta/auto-memory` for reflection subagents and reused shell analysis for repeated Bash approval rules ([#1888](https://github.com/letta-ai/letta-code/pull/1888), [#1892](https://github.com/letta-ai/letta-code/pull/1892))
- Removed the built-in `explore` subagent ([#1896](https://github.com/letta-ai/letta-code/pull/1896))
- Added GPT-5.5 ChatGPT BYOK models and auto-approval for safe `git grep` commands ([#1901](https://github.com/letta-ai/letta-code/pull/1901), [#1900](https://github.com/letta-ai/letta-code/pull/1900))
- Added optional inbound debounce for Slack messages and supported proactive Slack `MessageChannel` targets ([#1891](https://github.com/letta-ai/letta-code/pull/1891), [#1889](https://github.com/letta-ai/letta-code/pull/1889), [#1898](https://github.com/letta-ai/letta-code/pull/1898))
- Posted Slack lifecycle errors in-thread ([#1893](https://github.com/letta-ai/letta-code/pull/1893))
- Removed the periodic memory-sync reminder injection ([#1910](https://github.com/letta-ai/letta-code/pull/1910))
- Cleared stale `origin` push URLs during memory remote repair and stored reflection payload snapshots under the transcript root ([#1908](https://github.com/letta-ai/letta-code/pull/1908), [#1912](https://github.com/letta-ai/letta-code/pull/1912))
- Normalized outgoing base64 image media types ([#1909](https://github.com/letta-ai/letta-code/pull/1909))

## 0.23.11

- Stamped ISO 8601 timestamps on all stream-JSON wire events ([#1867](https://github.com/letta-ai/letta-code/pull/1867))
- Made forked subagents stop continuing parent tasks and propagated parent scope with clearer memory-mode shell constraints ([#1875](https://github.com/letta-ai/letta-code/pull/1875), [#1870](https://github.com/letta-ai/letta-code/pull/1870))
- Scoped the reflection gate by parent agent and conversation and unified auto-denial message formatting ([#1882](https://github.com/letta-ai/letta-code/pull/1882), [#1871](https://github.com/letta-ai/letta-code/pull/1871))
- Allowed git branch filter flags in plan mode’s read-only check ([#1879](https://github.com/letta-ai/letta-code/pull/1879))
- Denied stale restored client approvals and loosened the `system_alert` guard so compaction summaries don’t leak as user messages ([#1876](https://github.com/letta-ai/letta-code/pull/1876), [#1885](https://github.com/letta-ai/letta-code/pull/1885))
- Used `.json` extensions for reflection payload files, recorded real agent and message IDs in reflection telemetry, and clarified secret reminder text and redaction placeholders ([#1880](https://github.com/letta-ai/letta-code/pull/1880), [#1874](https://github.com/letta-ai/letta-code/pull/1874), [#1884](https://github.com/letta-ai/letta-code/pull/1884))
- Isolated runtime scope for tool execution, hardened image-resize verification, and improved the clipboard screenshot fallback ([#1873](https://github.com/letta-ai/letta-code/pull/1873), [#1872](https://github.com/letta-ai/letta-code/pull/1872), [#1877](https://github.com/letta-ai/letta-code/pull/1877))

## 0.23.10

- Added the Discord channel plugin ([#1825](https://github.com/letta-ai/letta-code/pull/1825))
- Added Telegram memo transcription via Whisper ([#1806](https://github.com/letta-ai/letta-code/pull/1806))
- Added `grep_in_files` content-search command and global memory history with commit-diff retrieval over WebSocket ([#1857](https://github.com/letta-ai/letta-code/pull/1857), [#1864](https://github.com/letta-ai/letta-code/pull/1864), [#1866](https://github.com/letta-ai/letta-code/pull/1866))
- Added the `update_toolset` WebSocket command for the desktop UI ([#1794](https://github.com/letta-ai/letta-code/pull/1794))
- Renamed reflection to “dream” in the TUI ([#1856](https://github.com/letta-ai/letta-code/pull/1856))
- Respected `--no-system-info-reminder` for agent-info reminders ([#1858](https://github.com/letta-ai/letta-code/pull/1858))
- Preserved Slack threaded replies across message subtypes ([#1863](https://github.com/letta-ai/letta-code/pull/1863))
- Warned when `/logout` leaves an env API key in place ([#1819](https://github.com/letta-ai/letta-code/pull/1819))

## 0.23.9

- Added Kimi K2.6 ([#1851](https://github.com/letta-ai/letta-code/pull/1851))
- Added cross-agent memory guard for permissions and an opt-in `x-letta-node` header via the `LETTA_NODE` environment variable ([#1852](https://github.com/letta-ai/letta-code/pull/1852), [#1835](https://github.com/letta-ai/letta-code/pull/1835))
- Created hidden conversations for agent-to-agent and forked-subagent paths ([#1838](https://github.com/letta-ai/letta-code/pull/1838))
- Replayed memory writes on remote MemFS conflicts ([#1853](https://github.com/letta-ai/letta-code/pull/1853))
- Scoped the worktree watcher correctly and prevented `@` autocomplete from cancelling backspace searches ([#1842](https://github.com/letta-ai/letta-code/pull/1842), [#1850](https://github.com/letta-ai/letta-code/pull/1850))

## 0.23.8

- Recovered pending channel approvals after a listener reconnect ([#1833](https://github.com/letta-ai/letta-code/pull/1833))
- Supported the `AUTO_MEMORY` model override for reflection subagents ([#1836](https://github.com/letta-ai/letta-code/pull/1836))

## 0.23.7

- Handled interactive approvals in channel-routed chats ([#1831](https://github.com/letta-ai/letta-code/pull/1831))
- Handled PID recycling in the container scheduler lease ([#1808](https://github.com/letta-ai/letta-code/pull/1808))

## 0.23.6

- Added the `letta channels bind` CLI command ([#1802](https://github.com/letta-ai/letta-code/pull/1802))
- Added a Slack default permission mode and bootstrapped mention-created thread context ([#1812](https://github.com/letta-ai/letta-code/pull/1812), [#1811](https://github.com/letta-ai/letta-code/pull/1811))
- Streamed bash output over `stream_delta` ([#1799](https://github.com/letta-ai/letta-code/pull/1799))
- Removed the 3-day auto-expiry for recurring cron tasks ([#1828](https://github.com/letta-ai/letta-code/pull/1828))
- Added `--no-bin-links` for Windows channel runtime installs ([#1824](https://github.com/letta-ai/letta-code/pull/1824))
- Clarified Opus 4.7 reasoning tiers and moved the `opus` handle to Opus 4.7 ([#1816](https://github.com/letta-ai/letta-code/pull/1816), [#1818](https://github.com/letta-ai/letta-code/pull/1818))
- Added hybrid file-index directory listing ([#1817](https://github.com/letta-ai/letta-code/pull/1817))

## 0.23.5

- Added Opus 4.7 ([#1814](https://github.com/letta-ai/letta-code/pull/1814))
- Added channel turn lifecycle hooks ([#1807](https://github.com/letta-ai/letta-code/pull/1807))
- Separated MemFS state from local checkout ([#1800](https://github.com/letta-ai/letta-code/pull/1800))
- Hydrated prior Slack thread context on first mention and disabled outbound web-client retries ([#1803](https://github.com/letta-ai/letta-code/pull/1803), [#1804](https://github.com/letta-ai/letta-code/pull/1804))
- Launched dev subagents with text loaders for prompt files and synced conversation refs for bootstrap reminders ([#1796](https://github.com/letta-ai/letta-code/pull/1796), [#1805](https://github.com/letta-ai/letta-code/pull/1805))

## 0.23.4

- Scoped `MessageChannel` to bound conversations ([#1793](https://github.com/letta-ai/letta-code/pull/1793))

## 0.23.3

- Made the `recall` subagent fork the parent conversation ([#1787](https://github.com/letta-ai/letta-code/pull/1787))
- Unified `MessageChannel` discovery, deduped Slack threaded mention ingress, and returned account snapshots before live refresh ([#1788](https://github.com/letta-ai/letta-code/pull/1788), [#1789](https://github.com/letta-ai/letta-code/pull/1789), [#1790](https://github.com/letta-ai/letta-code/pull/1790))
- Preserved queued user OTIDs across listener dequeue and send ([#1791](https://github.com/letta-ai/letta-code/pull/1791))

## 0.23.2

- Initiated file indexing on app load ([#1785](https://github.com/letta-ai/letta-code/pull/1785))
- Resolved the Slack Bolt App constructor from the bundled runtime ([#1784](https://github.com/letta-ai/letta-code/pull/1784))

## 0.23.1

- Added a current-working-directory watcher for auto-detection ([#1778](https://github.com/letta-ai/letta-code/pull/1778))
- Applied real-time sync for the filesystem ([#1755](https://github.com/letta-ai/letta-code/pull/1755))
- Restored enabled channel adapters on startup ([#1782](https://github.com/letta-ai/letta-code/pull/1782))

## 0.23.0

- Added the Slack channel adapter with account-scoped channel management and Telegram media + reaction parity ([#1763](https://github.com/letta-ai/letta-code/pull/1763), [#1774](https://github.com/letta-ai/letta-code/pull/1774), [#1780](https://github.com/letta-ai/letta-code/pull/1780))
- Installed the Telegram runtime on demand ([#1768](https://github.com/letta-ai/letta-code/pull/1768))
- Generalized core channel seams and improved shell command UI remapping ([#1762](https://github.com/letta-ai/letta-code/pull/1762), [#1758](https://github.com/letta-ai/letta-code/pull/1758))
- Allowed read-only shell inspection scripts in permissions and preserved shell command semantic labels across chained Bash commands ([#1766](https://github.com/letta-ai/letta-code/pull/1766), [#1767](https://github.com/letta-ai/letta-code/pull/1767))
- Extracted a shared shell analysis layer for the permission system ([#1769](https://github.com/letta-ai/letta-code/pull/1769))
- Filtered reflection payloads and switched them to JSON format ([#1779](https://github.com/letta-ai/letta-code/pull/1779))
- Scoped `Skill` lookup to the executing listener turn ([#1770](https://github.com/letta-ai/letta-code/pull/1770))

## 0.22.4

- Fixed repeated Linux keychain read warnings during auth setup ([#1663](https://github.com/letta-ai/letta-code/pull/1663))
- Fixed CLI subcommands so they dispatch before the TUI initializes, and fixed `letta listen` startup ordering so settings load before telemetry ([#1725](https://github.com/letta-ai/letta-code/pull/1725), [#1752](https://github.com/letta-ai/letta-code/pull/1752))
- Added outbound Telegram markdown formatting and hardened Telegram reminder delivery in channels mode ([#1754](https://github.com/letta-ai/letta-code/pull/1754), [#1756](https://github.com/letta-ai/letta-code/pull/1756), [#1757](https://github.com/letta-ai/letta-code/pull/1757))

## 0.22.3

- Added OAuth device flow for headless server deployments ([#1731](https://github.com/letta-ai/letta-code/pull/1731))
- Fixed memory git commits to unstage paths after commit-hook failures ([#1734](https://github.com/letta-ai/letta-code/pull/1734))
- Fixed bundled CLI packaging to externalize grammY correctly ([#1749](https://github.com/letta-ai/letta-code/pull/1749))

## 0.22.2

- Fixed the pre-commit frontmatter validator to ignore YAML continuation lines ([#1743](https://github.com/letta-ai/letta-code/pull/1743))
- Improved inbound channel reply prompting and OAuth setup network error messages ([#1746](https://github.com/letta-ai/letta-code/pull/1746), [#1747](https://github.com/letta-ai/letta-code/pull/1747))

## 0.22.1

- Added live websocket channel management for channels mode ([#1744](https://github.com/letta-ai/letta-code/pull/1744))

## 0.22.0

- Added the channels system with a Telegram MVP in listener/WebSocket mode ([#1737](https://github.com/letta-ai/letta-code/pull/1737))
- Stopped sending self-hosted errors to telemetry ([#1730](https://github.com/letta-ai/letta-code/pull/1730))
- Fixed `ExitPlanMode` to restore the correct default permission mode and aligned listener task notification queue semantics ([#1738](https://github.com/letta-ai/letta-code/pull/1738), [#1739](https://github.com/letta-ai/letta-code/pull/1739))

## 0.21.18

- Added the `scheduling-tasks` built-in skill for cron-style reminders and automations ([#1714](https://github.com/letta-ai/letta-code/pull/1714))
- Added the `/btw` command for forked conversation side-queries and device-side file watching with `watch_file` / `unwatch_file` ([#1596](https://github.com/letta-ai/letta-code/pull/1596), [#1718](https://github.com/letta-ai/letta-code/pull/1718))
- Added web history search filters and content-search mode in the history tab ([#1681](https://github.com/letta-ai/letta-code/pull/1681), [#1683](https://github.com/letta-ai/letta-code/pull/1683))
- Added Opus 1M LC support and improved 1M context window handling ([#1701](https://github.com/letta-ai/letta-code/pull/1701), [#1720](https://github.com/letta-ai/letta-code/pull/1720))
- Fixed memory sync, permissions, and tool behavior across runtimes, including Windows git credential helpers, memory tool schema alignment, `apply_patch` semantics, and shell truncation behavior ([#1700](https://github.com/letta-ai/letta-code/pull/1700), [#1702](https://github.com/letta-ai/letta-code/pull/1702), [#1704](https://github.com/letta-ai/letta-code/pull/1704), [#1709](https://github.com/letta-ai/letta-code/pull/1709), [#1710](https://github.com/letta-ai/letta-code/pull/1710), [#1711](https://github.com/letta-ai/letta-code/pull/1711), [#1721](https://github.com/letta-ai/letta-code/pull/1721))

## 0.21.17

- Added per-personality default models and set the `kawaii` personality to prefer `auto-chat` ([#1687](https://github.com/letta-ai/letta-code/pull/1687))
- Added the `glm-5.1` model preset ([#1694](https://github.com/letta-ai/letta-code/pull/1694))
- Enforced git worktree creation under `.letta/worktrees/` ([#1693](https://github.com/letta-ai/letta-code/pull/1693))
- Fixed first-connection bootstrap of base tools, desktop file indexer visibility, and memory-tool auto-approval behavior in `acceptEdits` mode ([#1684](https://github.com/letta-ai/letta-code/pull/1684), [#1689](https://github.com/letta-ai/letta-code/pull/1689), [#1690](https://github.com/letta-ai/letta-code/pull/1690))
- Improved memfs push reliability, model-setting context-window updates, and websocket listener hot-path performance ([#1688](https://github.com/letta-ai/letta-code/pull/1688), [#1660](https://github.com/letta-ai/letta-code/pull/1660), [#1695](https://github.com/letta-ai/letta-code/pull/1695))

## 0.21.16

- Added `memory_history` and `memory_file_at_ref` device commands for memory inspection ([#1637](https://github.com/letta-ai/letta-code/pull/1637))
- Fixed memfs clone/pull to retry on transient 52x git errors ([#1675](https://github.com/letta-ai/letta-code/pull/1675))
- Disabled auto-init for newly created agents ([#1679](https://github.com/letta-ai/letta-code/pull/1679))

## 0.21.15

- Improved insufficient-credits error copy for CLI flows ([#1672](https://github.com/letta-ai/letta-code/pull/1672))
- Retried formatted Cloudflare `521` errors during recovery ([#1674](https://github.com/letta-ai/letta-code/pull/1674))

## 0.21.14

- Stopped sync recovery failures from spamming the transcript in listener mode ([#1669](https://github.com/letta-ai/letta-code/pull/1669))
- Fixed websocket stream retries to relay abort signals correctly ([#1668](https://github.com/letta-ai/letta-code/pull/1668))

## 0.21.13

- Fixed memfs skill lookup in the `Skill` tool ([#1649](https://github.com/letta-ai/letta-code/pull/1649))
- Fixed memory-directory git commits to use the agent git identity ([#1640](https://github.com/letta-ai/letta-code/pull/1640))
- Refreshed listener loop status when the active plan file path changes ([#1666](https://github.com/letta-ai/letta-code/pull/1666))

## 0.21.12

- Added plan file path tracking in listener loop state ([#1662](https://github.com/letta-ai/letta-code/pull/1662))
- Scoped memory subagents to memory roots for safer permissions ([#1656](https://github.com/letta-ai/letta-code/pull/1656))
- Updated the `working-in-parallel` skill with pre-commit hook guidance ([#1655](https://github.com/letta-ai/letta-code/pull/1655))

## 0.21.11

- Preserved websocket loop error details in listener mode ([#1650](https://github.com/letta-ai/letta-code/pull/1650))
- Fixed hidden approvals to unwind correctly after interrupts ([#1657](https://github.com/letta-ai/letta-code/pull/1657))

## 0.21.10

- Fixed listener approval request projection to be atomic ([#1644](https://github.com/letta-ai/letta-code/pull/1644))
- Fixed listener transcripts to suppress stale approval recovery notices and show full `update_subagents` status updates ([#1641](https://github.com/letta-ai/letta-code/pull/1641), [#1643](https://github.com/letta-ai/letta-code/pull/1643))
- Added `[[path]]` indexing guidance to the system prompt and memory tool docs ([#1642](https://github.com/letta-ai/letta-code/pull/1642))

## 0.21.9

- Added websocket approval suggestion support in listener mode ([#1629](https://github.com/letta-ai/letta-code/pull/1629))

## 0.21.8

- Improved file indexing correctness, Merkle propagation, and freshness ([#1615](https://github.com/letta-ai/letta-code/pull/1615))
- Fixed `/fork` for default conversations to pass `agent_id`, and kept auto models on the default toolset ([#1617](https://github.com/letta-ai/letta-code/pull/1617), [#1618](https://github.com/letta-ai/letta-code/pull/1618))
- Fixed self-hosted model fallback for new agents and improved secret prompting ([#1619](https://github.com/letta-ai/letta-code/pull/1619), [#1623](https://github.com/letta-ai/letta-code/pull/1623))
- Fixed approval recovery so restored approvals continue through the live pipeline without max-turn exits ([#1622](https://github.com/letta-ai/letta-code/pull/1622), [#1625](https://github.com/letta-ai/letta-code/pull/1625))
- Fixed websocket listener retention leaks, agent info reminder metadata, and miscellaneous permissions issues ([#1624](https://github.com/letta-ai/letta-code/pull/1624), [#1627](https://github.com/letta-ai/letta-code/pull/1627), [#1628](https://github.com/letta-ai/letta-code/pull/1628))

## 0.21.7

- Added the `/empanada` slash command for Empanada Empire ordering ([#1612](https://github.com/letta-ai/letta-code/pull/1612))

## 0.21.6

- Changed `/init` to use the new context constitution workflow for deeper memory initialization ([#1608](https://github.com/letta-ai/letta-code/pull/1608))
- Changed `history-analyzer` to use the same context constitution principles during history migration ([#1610](https://github.com/letta-ai/letta-code/pull/1610))
- Added `add-agent` support to server-mode websocket clients ([#1606](https://github.com/letta-ai/letta-code/pull/1606))
- Fixed duplicate OpenAI GPT-5.4 presets in model selection ([#1607](https://github.com/letta-ai/letta-code/pull/1607))
- Fixed `AskUserQuestion` and `ExitPlanMode` approvals to preserve the user’s draft input ([#1570](https://github.com/letta-ai/letta-code/pull/1570))

## 0.21.5

- Added `/personality` to swap between curated agent personality presets ([#1439](https://github.com/letta-ai/letta-code/pull/1439))
- Added `letta agents create` with `--personality`, `--description`, `--tags`, and `--pinned` options ([#1571](https://github.com/letta-ai/letta-code/pull/1571))
- Changed session history storage to use `~/.letta/` instead of `~/.letta-code/` ([#1588](https://github.com/letta-ai/letta-code/pull/1588))
- Added remote `/init`, richer git branch context, and improved client-side file editing in server mode ([#1600](https://github.com/letta-ai/letta-code/pull/1600), [#1556](https://github.com/letta-ai/letta-code/pull/1556), [#1589](https://github.com/letta-ai/letta-code/pull/1589))
- Added Bedrock fallback when Anthropic is unavailable ([#1569](https://github.com/letta-ai/letta-code/pull/1569))
- Fixed headless 409 recovery, no-op commit message creation, queued task notifications, and per-conversation subagent state in server mode ([#1591](https://github.com/letta-ai/letta-code/pull/1591), [#1598](https://github.com/letta-ai/letta-code/pull/1598), [#1595](https://github.com/letta-ai/letta-code/pull/1595), [#1602](https://github.com/letta-ai/letta-code/pull/1602))

## 0.21.4

- No notable user-facing changes in this release

## 0.21.3

- Added websocket `list_models` and `update_model` support for server-mode clients ([#1579](https://github.com/letta-ai/letta-code/pull/1579))
- Improved remote reflection progress updates with step counts, and fixed follow-up model update status messages ([#1578](https://github.com/letta-ai/letta-code/pull/1578), [#1582](https://github.com/letta-ai/letta-code/pull/1582))

## 0.21.2

- Added advertised `supported_commands` in device status and remote `/doctor` command support for server-mode clients ([#1568](https://github.com/letta-ai/letta-code/pull/1568), [#1572](https://github.com/letta-ai/letta-code/pull/1572))
- Added websocket reflection and sleeptime parity in server mode ([#1567](https://github.com/letta-ai/letta-code/pull/1567))
- Added remote skill enable/disable controls ([#1573](https://github.com/letta-ai/letta-code/pull/1573))
- Improved `/resume` to fetch only the messages it needs when resuming conversations ([#1550](https://github.com/letta-ai/letta-code/pull/1550))

## 0.21.1

- Fixed bundled skills to resolve script paths consistently across installations ([#1563](https://github.com/letta-ai/letta-code/pull/1563))

## 0.21.0

- Added `CONVERSATION_ID` to shell tool environments and agent info reminders ([#1557](https://github.com/letta-ai/letta-code/pull/1557))
- Improved message search performance by fetching active results before prefetching ([#1553](https://github.com/letta-ai/letta-code/pull/1553))

## 0.19.11

- Added provider status page links on downstream model errors ([#1523](https://github.com/letta-ai/letta-code/pull/1523))
- Added Baseten Kimi model support and client-side file editing support ([#1529](https://github.com/letta-ai/letta-code/pull/1529), [#1544](https://github.com/letta-ai/letta-code/pull/1544))
- Added optional `/fork` summaries and a `fork` subagent type that inherits the full parent conversation context ([#1530](https://github.com/letta-ai/letta-code/pull/1530), [#1539](https://github.com/letta-ai/letta-code/pull/1539))
- Added server-mode `/init`, memfs sync on first message, and session-context reminders in listener mode ([#1534](https://github.com/letta-ai/letta-code/pull/1534), [#1546](https://github.com/letta-ai/letta-code/pull/1546), [#1536](https://github.com/letta-ai/letta-code/pull/1536))
- Fixed large-workspace file indexing OOMs and improved transient 521 recovery in remote mode ([#1533](https://github.com/letta-ai/letta-code/pull/1533), [#1552](https://github.com/letta-ai/letta-code/pull/1552))

## 0.19.10

- Fixed server-mode approval replay after interrupts ([#1521](https://github.com/letta-ai/letta-code/pull/1521))

## 0.19.9

- Added the `/secret` slash command for managing shell-command secrets ([#1435](https://github.com/letta-ai/letta-code/pull/1435))
- Added `/fork` to duplicate the current conversation into a new thread ([#1517](https://github.com/letta-ai/letta-code/pull/1517))
- Added automatic fallback to `letta/auto` when quota limits block the current model ([#1473](https://github.com/letta-ai/letta-code/pull/1473))
- Fixed conversation restore and persistence when resuming with `--agent` or `--name`, and kept `search_files` scoped to the current conversation cwd ([#1514](https://github.com/letta-ai/letta-code/pull/1514), [#1515](https://github.com/letta-ai/letta-code/pull/1515), [#1512](https://github.com/letta-ai/letta-code/pull/1512))
- Fixed websocket resume, streaming recovery, and background task notifications in server mode ([#1500](https://github.com/letta-ai/letta-code/pull/1500), [#1505](https://github.com/letta-ai/letta-code/pull/1505), [#1520](https://github.com/letta-ai/letta-code/pull/1520))

## 0.19.8

- Added the `/doctor` command to audit and refine an agent’s memory structure ([#1488](https://github.com/letta-ai/letta-code/pull/1488))
- Added client-side `memory_apply_patch` support for Codex toolsets, complementing the existing `memory` tool ([#1485](https://github.com/letta-ai/letta-code/pull/1485))
- Added memory tool event updates so connected clients can refresh memory state automatically ([#1495](https://github.com/letta-ai/letta-code/pull/1495))
- Improved `/resume` with progressive loading for large conversation lists ([#1462](https://github.com/letta-ai/letta-code/pull/1462))
- Fixed listener permission recovery, queued skill replay, retry deduplication, and related websocket resume issues ([#1492](https://github.com/letta-ai/letta-code/pull/1492), [#1499](https://github.com/letta-ai/letta-code/pull/1499), [#1502](https://github.com/letta-ai/letta-code/pull/1502), [#1478](https://github.com/letta-ai/letta-code/pull/1478))

## 0.19.7

- Changed `/init` guidance to remove hard-coded memory file count and size targets ([#1483](https://github.com/letta-ai/letta-code/pull/1483))
- Changed memory file frontmatter so `description` is required while legacy `limit` remains optional ([#1484](https://github.com/letta-ai/letta-code/pull/1484))
- Added pre-commit validation for memory and skill formatting ([#1482](https://github.com/letta-ai/letta-code/pull/1482))
- Improved reflection snapshots by collapsing very large directories in the memory tree ([#1481](https://github.com/letta-ai/letta-code/pull/1481))

## 0.19.6

- Added MiniMax 2.7 as a supported model preset ([#1453](https://github.com/letta-ai/letta-code/pull/1453))
- Added optional conversation naming to `/new` ([#1451](https://github.com/letta-ai/letta-code/pull/1451))
- Changed `/search` to default to the current agent scope ([#1450](https://github.com/letta-ai/letta-code/pull/1450))
- Changed Letta Code to remove the `--continue` flag and rely on default resume, `--new`, `--resume`, and `--conversation` instead ([#1458](https://github.com/letta-ai/letta-code/pull/1458))
- Improved startup resume behavior for project-specific conversations and auto model routing context windows ([#1457](https://github.com/letta-ai/letta-code/pull/1457), [#1463](https://github.com/letta-ai/letta-code/pull/1463))

## 0.19.5

- Changed `/resume` to sort conversations by most recent activity first ([#1444](https://github.com/letta-ai/letta-code/pull/1444))
- Fixed `LETTA_DEBUG` environment variable handling so debug logging is respected when set ([#1452](https://github.com/letta-ai/letta-code/pull/1452))

## 0.19.4

- Added the `memory` tool back to the default Claude, Codex, and Gemini toolsets ([#1447](https://github.com/letta-ai/letta-code/pull/1447))
- Fixed Electron and Node.js environments to fall back to `node-pty` when Bun is unavailable ([#1446](https://github.com/letta-ai/letta-code/pull/1446))
- Fixed listener approval reentry so queued turns drain correctly after approval recovery ([#1448](https://github.com/letta-ai/letta-code/pull/1448))

## 0.19.3

- Added Kitty keyboard protocol support for more reliable key handling in supported terminals ([#1334](https://github.com/letta-ai/letta-code/pull/1334))
- Added separate BYOK support for zAI Coding Plan accounts via `/connect zai-coding` ([#1434](https://github.com/letta-ai/letta-code/pull/1434))
- Changed `ExitPlanMode` to always require manual approval, even in `--yolo` mode ([#1440](https://github.com/letta-ai/letta-code/pull/1440))
- Fixed approval comments being preserved in tool responses for listener and client-tool integrations ([#1441](https://github.com/letta-ai/letta-code/pull/1441), [#1442](https://github.com/letta-ai/letta-code/pull/1442), [#1443](https://github.com/letta-ai/letta-code/pull/1443))
- Fixed permission mode sync issues in desktop listener sessions ([#1432](https://github.com/letta-ai/letta-code/pull/1432), [#1437](https://github.com/letta-ai/letta-code/pull/1437))

## 0.19.2

- Fixed TUI live-preview flicker with post-highlight clipping ([#1423](https://github.com/letta-ai/letta-code/pull/1423))
- Changed default model selection to prefer `auto` instead of Sonnet ([#1429](https://github.com/letta-ai/letta-code/pull/1429))
- Fixed V2 listener terminal event wiring and required approval for `ExitPlanMode` in bypass mode ([#1430](https://github.com/letta-ai/letta-code/pull/1430), [#1431](https://github.com/letta-ai/letta-code/pull/1431))

## 0.19.1

- In [Remote environments](/platform/computers/byom/index.md), `letta server` now keeps [permission modes](/configuration/permissions/index.md) separate per conversation, and restores each conversation’s working directory and permission mode after a server restart
- Added GPT-5.4 Mini and GPT-5.4 Nano model presets for OpenAI and ChatGPT Plus/Pro in [Models](/configuration/models/index.md)
- Fixed [custom subagents](/configuration/subagents/index.md) loading when `.md` files use Windows line endings or a UTF-8 BOM in frontmatter
- Fixed duplicate bypass auto-approvals in plan mode when the same tool call is replayed

## 0.19.0

- Added a new `/recompile` slash command to recompile the current agent and conversation when you need to refresh prompt state manually
- Added a client-side `memory` tool with git-backed sync for MemFS workflows, plus startup warnings when context repositories are not enabled
- Changed built-in default agents and subagents to prefer auto model routing when available, with safer self-hosted fallbacks
- Improved `/init` so shallow initialization adapts to your existing memory structure instead of assuming a fresh layout
- Improved server mode listener sessions by scoping runtime state per conversation for more reliable parallel and resumed sessions
- Fixed startup reconciliation for attached base tools and default summarization model settings on existing agents
- Fixed status line refresh behavior and several subagent lifecycle and display issues

## 0.18.3

- Added indexed `@` file search with persistent cache support
- Added `.letta/.lettaignore` support and `MAX_ENTRIES` tuning in `~/.letta/.lettasettings` for file search indexing
- Added source-faithful system prompt presets: `source-claude`, `source-codex`, and `source-gemini`
- Added bundled `dispatching-coding-agents` skill
- Added PTY terminal session support in `letta server` listener mode
- Added `recover_pending_approvals` support in headless `--input-format stream-json` control requests
- Added `gpt-5-mini-high` model preset
- Changed `/init` to run through the primary agent as an interactive initialization flow
- Improved shallow auto-init performance
- Improved reflection subagent context by reading local transcript files
- Improved `letta server` working-directory and environment cache persistence across restarts
- Fixed model preset refresh and update-args fallback handling to preserve context window settings and BYOK compatibility
- Fixed pre-stream `409 CONFLICT` busy handling to resume server-side runs
- Fixed newly spawned subagents to default `memfs` to off

## 0.18.2

- Fixed a Bun/Linux crash in vendored Ink input handling when `handleData` receives undefined input

## 0.18.1

- Added syntax highlighting for Bash command previews in approval and tool-call UI
- Improved diff rendering with syntax-highlighted output in the TUI
- Fixed missing backfilled tool calls in streamed history rendering
- Fixed plan file path race during `ExitPlanMode`
- Fixed `--yolo` auto-approval while plan mode is active
- Fixed leading-space artifacts on wrapped continuation lines in TUI text
- Fixed token counting display in subagent status panels

## 0.18.0

- Added recipe-based system prompt management
- Added client-side skills loading and skill reminders
- Added per-conversation working directories in server mode listener sessions
- Added minimum Docker server version checks with upgrade guidance
- Added `conversation_id` propagation on WebSocket listener events
- Added plan mode system reminders in server mode
- Added command hints for agents using non-default system prompts
- Added ChatGPT Plus/Pro `gpt-5.4-fast` model tier support
- Fixed Gemini 3.1 Pro Preview model handles
- Fixed custom BYOK models not appearing in `/model` selector
- Fixed listener queue pump recovery and parity in server mode
- Fixed `ExitPlanMode` continuation across permission mode cycling

## 0.17.2

- Added GPT-5.4, GPT-5.4 Fast, and GPT-5.4 Pro model support
- Added `(Beta)` label to `letta/auto` and `letta/auto-fast` in model selector
- Added blinking spinner for background subagent indicator in footer
- Added `run_request_error` event in `letta remote` when initial POST fails
- Excluded `AskUserQuestion` from headless mode toolset
- Changed `default` system prompt preset to use the Letta system prompt instead of `letta-claude`
- Changed free-tier default model from MiniMax M2.5 to GLM-5
- Fixed `--system` flag to validate against known preset IDs instead of silently falling back
- Fixed conversation model overrides not persisting across turns
- Fixed conversation model override cleared on transient retrieve errors
- Fixed stale `max_tokens` values lingering after model switch
- Fixed `letta remote` interrupt recovery and reconnect hydration
- Fixed `letta remote` stale approval conflicts after stop-reason errors
- Fixed footer subagent link and alignment
- Removed `--system-append` flag

## 0.17.0

- Renamed `letta remote` to `letta server` (with `remote` kept as an alias)
- Added `letta/auto` and `letta/auto-fast` model support in model selection
- Added max (`xhigh`) reasoning tiers for Sonnet 4.6 and Opus 4.6
- Added none/low/medium/high reasoning tiers for Opus 4.5
- Added auto-init memory bootstrap on first message for new MemFS agents
- Changed `/init` to use shallow and deep initialization tiers
- Added subagent type tags when creating new subagents
- Added `agent_id`, `conversation_id`, and `last_run_id` to `/statusline` payloads
- Added agent-aware `/rename` hints in command-IO reminders
- Changed app URL generation to use centralized `/chat` links
- Fixed headless `409 CONFLICT` busy retries to use exponential backoff
- Fixed startup guard for missing default conversation IDs
- Fixed default-conversation API routing for SDK 1.7.11 (`conversation_id="default"` with `agent_id`)
- Improved readability of command-IO and toolset-change reminders

## 0.16.15

- Added unified provider normalization for `/connect` and `letta connect`
- Added `chatgpt` as canonical connect provider token (`codex` remains an alias)
- Added background agent indicator in the footer
- Added `background_agents` in `/statusline` payloads
- Added listener version metadata in `letta remote` registration
- Changed default model from Sonnet 4.5 to Sonnet 4.6
- Fixed `Shift+Tab` to enter plan mode before auto-approve
- Fixed `letta remote` re-registration to recover instead of crash
- Fixed `/model` selection persistence for default conversations
- Improved idle-time flushing of background subagent notifications
- Improved `approve-always` pattern generation for read-only `gh` commands

## 0.16.14

- Added `/compaction` command for interactively selecting compaction mode
- Added `--debug` flag to `letta remote` for plain-text console logging
- Added always-on session log written to `~/.letta/logs/remote/` for every `letta remote` session
- Added debug log file written to `~/.letta/logs/debug/` for diagnostics
- Changed `/init` to run as a background subagent (non-blocking initialization)
- Changed reflection subagent output to be silenced from the primary agent’s context
- Fixed model selection not persisting when starting new conversations
- Fixed Bash tool git commit and PR instructions for Codex and Gemini toolsets

## 0.16.13

- Added update availability notifications in TUI and footer when a newer version is released
- Added `/compact self_compact_all` and `/compact self_compact_sliding_window` modes for agent-driven compaction
- Added `/reasoning-tab` command to toggle Tab key cycling through reasoning effort levels (opt-in, disabled by default)
- Added session usage details persistence shown in exit summary
- Removed `plan` subagent (plan mode no longer delegates to a dedicated subagent)
- Removed `defragmenting-memory` skill (memory subagent is now self-contained)
- Fixed `/clear` command to skip server-side message reset for named conversations
- Fixed `/model` and `/reasoning` commands to stay scoped to the current conversation
- Fixed plan mode permission level being reliably restored after exiting
- Fixed plan mode path handling with quote-aware shell parsing for `apply_patch` and scoped paths
- Fixed Cloudflare HTML 5xx errors handled gracefully with user-friendly messages
- Fixed ChatGPT `usage_limit_reached` errors to display the reset time
- Fixed API key caching to survive keychain failures mid-session
- Fixed clickable ADE and usage links in agent info bar
- Fixed `/model` selector to deduplicate models by handle
- Fixed model handle display removing `s:/t:` suffixes from status bar
- Fixed auto-open file viewers being skipped in SSH sessions
- Fixed memfs git credential helper value being redacted from debug logs
- Improved streaming resilience in `letta remote` mode

## 0.16.12

- Renamed `letta listen` command to `letta remote` (old name still works as an alias)
- Added automatic retry on empty LLM responses
- Fixed `--conv default` working alongside `--new-agent` flag
- Fixed approval data being preserved across stream resume boundaries
- Fixed TUI reflow glitches in footer and on terminal resize
- Fixed ADE link and streaming elapsed timer stability across terminal resizes

## 0.16.11

- Added GPT-5.3 Codex model tiers support
- Fixed WebSocket connectivity issue
- Fixed cosmetic display issue for newly created agents

## 0.16.10

- Simplified `letta listen` command: removed explicit binding flags and added auto-generated session names
- Fixed API key detection to read from environment variables rather than checking repo secrets
- Fixed memory defrag flow for git-backed memfs

## 0.16.9

- Fixed settings collision when running Letta Code from the home directory (project vs. global settings conflict)
- Updated featured models list to show only the latest frontier model per provider

## 0.16.8

- Fixed hooks not logging a full error stack trace when project settings are absent

## 0.16.7

- Added `/install-github-app` setup wizard for GitHub App integration
- Added `bootstrap_session_state` headless API for pre-configuring session state and memfs startup policy
- Fixed startup performance by skipping no-op preset refresh when resuming existing agents
- Fixed duplicate frontmatter blocks appearing in memory subagent prompt
- Fixed interactive tools from being auto-approved in listen mode
- Fixed headless `list_messages` to scope correctly to the default conversation
- Fixed last-character clipping on deferred-wrap terminals

## 0.16.6

- Fixed user permission settings path to use `~/.letta` instead of `~/.config/letta`

## 0.16.5

- Fixed default conversation sentinel handling in headless startup

## 0.16.4

- Added headless `list-messages` protocol command
- Fixed reasoning tag display when reasoning is set to none
- Disabled xhigh reasoning tier for Anthropic models

## 0.16.3

- Added `/palace` command alias for Memory Palace
- Added plan viewer with browser preview (opens plan markdown in browser)
- Added symlink support for skills installed in `~/.letta/skills/`
- Fixed Node 18 compatibility with `node:crypto` import
- Fixed `bypassPermissions` mode not persisting across transient retries
- Fixed transcript backfill on conversation resume
- Fixed assistant anchor recency on resume
- Fixed default conversation for freshly created subagents
- Fixed compaction reflection trigger for legacy summary format
- Fixed model preset settings not refreshing on resume

## 0.16.2

- Improved startup performance by eliminating redundant API calls
- Fixed slash commands blocked after interrupt during tool execution
- Fixed Memory Palace auto-open in tmux on macOS
- Fixed shared reminders disabled for subagents
- Fixed env var resolution in reflection/history-analyzer commit trailers
- Fixed Memory Palace nesting level display
- Fixed Memory Palace handling of `$` in memory content
- Fixed retry on quota limit errors

## 0.16.1

- Added Memory Palace static HTML viewer (opens memory visualization in browser from `/memfs`)
- Added auto-enable memfs from server-side tag on new machines
- Fixed error formatting for `/init`
- Fixed version reporting in feedback and telemetry
- Fixed headless mode defaulting to new conversation to prevent 409 race
- Fixed `/memory` command label to say “memory” instead of “memory blocks”
- Fixed `max_output_tokens` for GPT-5 reasoning variants
- Fixed LLM streaming error provider mapping

## 0.16.0

- Added reasoning settings step to `/model` selector for choosing reasoning tier after model selection
- Added Tab key cycling of reasoning tiers from the input area
- Added Sonnet 4.6 1M context window model variant
- Added Gemini 3.1 Pro Preview model support
- Added `auto` option for toolset mode with persistence across sessions
- Added `LETTA_MEMFS_LOCAL` env var to enable memfs on self-hosted servers
- Added Edit tool start line number in code diff display
- Added elapsed time display for running shell tools
- Added memory application guidance to system prompts
- Aligned TaskOutput display format with Bash output
- Fixed slash commands incorrectly opening state when no arguments are accepted
- Fixed ADE links for default conversation
- Fixed user settings being clobbered on save
- Fixed Gemini/GLM tools not working in plan mode
- Fixed permission mode desyncs in YOLO approval handling
- Fixed reasoning effort display in footer and model selector
- Fixed conversation routing after creating new agent in `/agents`
- Fixed plan file `apply_patch` paths not allowed in plan mode
- Fixed auto toolset detection for ChatGPT OAuth as Codex
- Fixed agents limit exceeded retry behavior
- Fixed default agent creation when base tools are missing
- Disabled hidden SDK retries for streaming POSTs
- Removed Sonnet 4.5 from featured models

## 0.15.6

- Added `sonnet` shortcut for Sonnet 4.6 model in `-m` flag

## 0.15.5

- Added Sonnet 4.6 model support (set as new default model)
- Changed featured model from Sonnet 4.5 to Sonnet 4.6

## 0.15.4

- Added `--skill-sources` flag to control which skill sources are enabled (comma-separated: `bundled`, `global`, `agent`, `project`, or `all`)
- Added `--no-bundled-skills` flag to disable only bundled skills while keeping other sources
- Added headless reflection settings: `--reflection-trigger`, `--reflection-behavior`, `--reflection-step-count`
- Added `--no-system-info-reminder` flag to suppress first-turn environment context reminder

## 0.15.3

- Added `MEMORY_DIR` and `AGENT_ID` environment variables exposed in shell tools
- Fixed ChatGPT connection and OAuth error retry classification
- Fixed slash command queueing while agent is running
- Fixed memfs/standard prompt section reconciliation
- Fixed auto-update execution and release gating
- Fixed interrupt timer reset on eager cancel
- Fixed skills reminders appearing in headless sessions
- Removed `max_turns` option from Task tool

## 0.15.2

- Added `/skills` command to browse available skills by source (bundled, global, agent, project)
- Added `memfs_enabled` status in headless init messages
- Fixed agent not being reused on directory switch (no longer creates unnecessary new agents)
- Fixed over-escaped strings in Edit tool
- Fixed memfs git pull authentication and credential URL normalization
- Fixed shell auto-approval path checks
- Fixed Windows absolute file-rule matching in permissions
- Fixed bundled JS subagent launcher on Windows
- Fixed model tier selection when model ID is selected directly

## 0.15.1

- Added `--no-skills` flag to disable bundled skills
- Added `--tags` flag for headless mode agent tagging
- Added MiniMax M2.5 model support
- Added specific retry messages for known LLM provider errors
- Improved reflection subagent to autonomously complete merge and push operations
- Removed `conversation_search` from default toolset
- Fixed ghost assistant messages when Anthropic returns `[text, thinking, text]` block order
- Fixed CONFLICT errors after interrupt during tool execution
- Fixed interrupt recovery to only trigger on real user interrupts
- Fixed memfs init steps in headless mode
- Fixed ADE default conversation link

## 0.15.0

- Added git-backed memory filesystem sync with automatic commit and push
- Added `reflection` subagent for background memory analysis and updates
- Added `history-analyzer` subagent and `migrating-from-codex-and-claude-code` skill for importing history from Claude Code and Codex CLIs
- Added `/statusline` command for configurable CLI footer status lines
- Added `/sleeptime` command for client-side reflection trigger settings
- Added `/compact [all|sliding_window]` mode options
- Added GLM-5 model support
- Renamed `/download` to `/export` and `--from-af` to `--import` (old names still work as aliases)
- Changed compaction to set summary as first message in conversation
- Fixed `@` file browser deep recursive search when browsing parent directories
- Fixed `/context` double rendering on short terminals
- Fixed system-reminder tag rendering in message backfill
- Fixed stream ID accumulator collisions

## 0.14.16

- Added custom tools support for SDK-side tool registration and execution in bidirectional mode
- Added agent registry import support (`@author/name` format for `--from-af`)
- Added `PreCompact` hooks now fire during server-side automatic compaction
- Fixed OpenAI encrypted content organization mismatch error handling
- Fixed headless pre-stream approval conflict recovery
- Fixed slash-prefixed messages without trailing space not being sendable
- Fixed model updates not sending `max_tokens` configuration to cloud
- Fixed memfs not detaching all memory tool variants when enabled
- Improved headless mode interactive tool behavior for bidirectional parity

## 0.14.15

- Added brand accent color for markdown link text
- Improved rendering stability and flicker prevention across footer and streaming status
- Improved always-allow behavior for skill script permissions
- Improved error guidance for model availability and credit issues
- Fixed `memory` defrag subagent to run in background
- Fixed MiniMax errors at higher token counts
- Fixed duplicate feedback command output on submit
- Fixed oversized shell tool output clipping in collapsed tool results
- Fixed task transcript propagation for max-step failures
- Removed ChatGPT OAuth Pro plan restriction for Codex connect

## 0.14.14

- Fixed `--max-turns` flag not accepted at top-level CLI
- Fixed subagent keychain migration churn

## 0.14.13

- Added GPT-5.3 Codex model support (ChatGPT Plus/Pro)
- Added permission mode restoration when exiting plan mode
- Fixed headless permission wait deadlock
- Fixed `/model` selection for shared-handle model tiers with different reasoning efforts
- Fixed subagent model display consistency

## 0.14.12

- Rewrote the Skill tool from load/unload commands to direct invocation (`skill: "name"` with optional `args`)
- Removed `skills` and `loaded_skills` memory blocks (skills are now listed in system-reminder messages)
- Added `--embedding` flag to specify embedding model when creating agents in headless mode
- Added `/context` command token usage breakdown by category (system, core memory, functions, messages)
- Added `showCompactions` setting to hide compaction messages (defaults to `false`)
- Added `LETTA_PACKAGE_MANAGER` env var to override detected package manager for auto-updates
- Changed featured model from Opus 4.5 to Opus 4.6
- Improved auto-updater to detect package manager (npm/bun/pnpm) instead of hardcoding npm
- Improved subagent auth to inherit credentials from parent, avoiding keychain contention
- Improved keychain availability check to use a non-mutating probe instead of set/delete
- Fixed `UserPromptSubmit` hook firing repeatedly on message dequeue
- Fixed `Stop` hook using first user message instead of most recent
- Removed `Setup` hook event type
- Updated memfs skill and system prompt

## 0.14.11

- Added prompt-based hooks that use an LLM to evaluate whether actions should be allowed or blocked
- Added `/context` command braille area chart showing token usage history across turns
- Added skills extraction and packaging for `--from-af` agent file imports
- Added `max_turns` parameter to Task tool for limiting subagent turn count
- Improved message queue to wait for tool completion instead of using a 15-second timeout
- Fixed Shift+Enter by normalizing newlines before keypress parsing
- Fixed keyboard protocol report filtering and scoped Linux Enter key handling
- Fixed `loaded_skills` block not resetting on new conversation
- Fixed memFS system prompt not updating based on `--memfs`/`--no-memfs` CLI flags
- Fixed empty assistant message bullets rendering
- Fixed skills directory path shown in extraction message
- Fixed subagent static promotion race during tool result reentry

## 0.14.10

- Added `/context` command to show context window usage with visual token bar
- Added background task support for `Task` and `Bash` tools via `run_in_background` parameter
- Added `TaskOutput` tool to retrieve output from background tasks
- Added `TaskStop` tool to stop running background tasks
- Added background task completion notifications injected into conversation
- Added `additionalContext` support for `PostToolUse` hooks (JSON output parsed for context injection)
- Added Claude Opus 4.6 model support
- Improved subagent status display with aligned dots, headers, and dimming for running agents
- Improved tool call dot phases and colors for clearer execution feedback
- Fixed `/download` command to pass `conversation_id` for non-default conversations

## 0.14.9

- Added number key support (1-9) to approval dialogs for quick selection
- Enabled memfs in headless mode when using `--agent` flag
- Fixed Enter key handling on Linux terminals that emit `\n` instead of `\r`
- Fixed error handling in headless bidirectional mode
- Fixed MCP skill templates with corrected paths
- Fixed malformed `AskUserQuestion` falling through to generic approval

## 0.14.8

- Added `converting-mcps-to-skills` bundled skill for connecting to MCP servers
- Added `PostToolUseFailure` hook that runs after tool failures (feeds stderr back to agent)
- Added `SessionEnd` hooks now run on Ctrl+C (SIGINT)
- Added conversation renaming when renaming agents via `/rename`
- Improved `SessionStart` hooks with feedback injection
- Improved post tool use feedback injection
- Fixed compaction display to show simple “Conversation compacted” message
- Fixed context windows fetched from server instead of hardcoded
- Fixed Windows PATH handling and PowerShell quoting
- Fixed thinking/assistant block spacing preservation during streaming
- Fixed logo resetting to flat frame when loading completes
- Fixed duplicate rendering of auto-approved file tools
- Fixed 409 “conversation busy” errors with exponential backoff
- Fixed flicker on tall approval dialogs

## 0.14.7

- Added trajectory stats tracking and completion summary on exit
- Improved `/memory` viewer to prioritize `system/` directory at top
- Fixed input area collapsing during approvals and selector overlays
- Fixed slash command menu render flicker
- Fixed rendering instability that caused line flicker

## 0.14.6

- Added alien art to command preview and exit message
- Added BYOK-aware model resolution with fallback for subagents
- Added network phase arrows to streaming status indicator
- Fixed handling of malformed `AskUserQuestion` data from LLM
- Fixed `/usage` command formatting
- Fixed `/memfs` position in command autocomplete order
- Fixed mojibake detection to preserve valid Unicode characters
- Fixed loading state layout consistency during startup
- Fixed autocomplete to show “No matching commands” instead of hiding
- Fixed `<Text>` encoding non-ASCII characters in Bun

## 0.14.5

- Added `--from-agent` flag for agent-to-agent communication in headless mode
- Refactored skill scripts into CLI subcommands (`letta memfs`, `letta blocks`, etc.)

## 0.14.4

- Added compaction messages display and new summary message type handling
- Fixed skill diffing code
- Fixed memfs skill scripts

## 0.14.3

- Fixed memfs frontmatter round-trip to preserve block metadata

## 0.14.2

- Fixed extra vertical spacing between memory block tabs
- Fixed Task tool approval dialogs to show full prompt
- Improved memfs sync performance

## 0.14.1

- Enabled Memory Filesystem (memfs) by default for newly created agents
- Added `--memfs` / `--no-memfs` CLI flags to control memfs on agent creation
- Fixed Bun string encoding issues

## 0.14.0

This release introduces **Memory Filesystem** (experimental) - your agent’s memory blocks now sync with local files in `.letta/memory/`, enabling direct editing and version control of agent memory.

### Memory Filesystem (experimental)

- Added Memory Filesystem (memfs) that syncs memory blocks with `.letta/memory/` directory
- Added agent-driven conflict resolution for memfs sync conflicts
- Added `/memfs` command to view sync status and resolve conflicts
- Added owner tags for tracking block ownership (system vs agent-created)
- Added hierarchical memory organization with `system/` prefix for core blocks
- Added `syncing-memory-filesystem` built-in skill for conflict resolution guidance
- Updated `/init` to create hierarchically organized memory blocks
- Updated `defragmenting-memory` skill to use memfs instead of backup/restore scripts

### New Models and Providers

- Added MiniMax M2.1 model support
- Added MiniMax BYOK support via `/connect`
- Added Kimi K2.5 model support
- Added OpenRouter BYOK support via `/connect`
- Added AWS Bedrock profile authentication method
- Added Bedrock Opus 4.5 fallback suggestion for Anthropic API errors

### Hooks Enhancements

- Added `UserPromptSubmit` hook that fires when user submits a prompt
- Added `reasoning` and `assistant_message` capture in `PostToolUse` and `Stop` hooks
- Added `LETTA_AGENT_ID` environment variable injection into hooks
- Added “Disable all hooks” toggle in `/hooks` command
- Added memory log hook example script

### Other Features

- Added agent-scoped skills directory (`~/.letta/agents/{id}/skills/`)
- Added user prompt message highlighting
- Added permissions status script
- Changed `conversation_search` to no longer be a default tool (use `recall` subagent instead)

### Fixes

- Fixed up/down arrow navigation with newlines in multi-line input
- Fixed cursor visibility on newline characters in multi-line input
- Fixed `@file` search to exclude `venv` and dependency directories
- Fixed `/feedback` command formatting and context
- Fixed approval dialog horizontal lines to extend full terminal width
- Fixed default agent creation on first bootup
- Fixed paste support in hooks TUI inputs
- Fixed hooks TUI with Enter to delete and better spacing
- Fixed help text for `letta --new` flag
- Fixed `UserPromptSubmit` hooks to not fire for slash commands
- Fixed subagents to be marked as hidden on creation
- Fixed LLM error retry to not retry 4xx client errors
- Fixed model selector display on self-hosted when default model unavailable

## 0.13.11

- Fixed agents limit exceeded error and added deletion support in `/agents`
- Fixed `-m` flag to correctly apply model variants with same handle

## 0.13.10

- Added AWS Bedrock support to `/connect` command
- Added multi-server support with settings indexed by server URL
- Added regex tool name matching for hooks (e.g., `"Edit|Write"`)
- Added message retry on premature interrupt
- Added desktop notification hook script
- Added `rm -rf` block hook script example
- Improved `/connect` command and model selector UX
- Disabled Incognito agent creation by default
- Fixed default model selection to use billing tier (free tier uses glm-4.7)
- Fixed self-hosted and localhost model selection during agent creation
- Fixed login screen styling to match other menus
- Fixed error message formatting

## 0.13.9

- Added Stop hook continuation on blocking (hook can keep agent working)
- Added example hook scripts for common patterns
- Improved `memory` subagent to produce hierarchical memory block structures
- Improved message queueing for smoother UX
- Fixed backfill failures to be handled gracefully instead of crashing

## 0.13.8

- Added search field to model selector (both Supported and All Available tabs)
- Fixed `/compact` to use correct conversations endpoint
- Fixed agent info bar layout to prevent overflow

## 0.13.7

- Added Claude Code-compatible hooks system with `/hooks` command for automating workflows
- Added cross-platform support for hooks executor (Windows, macOS, Linux)
- Added ViewImage tool for attaching local images to conversation context
- Added search field to model selector on both tabs
- Added Bedrock Opus 4.5 model
- Added conversation ID display in agent info bar
- Added immediate mode for interactive commands
- Improved cancellation with graceful 30s timeout before force-abort
- Fixed bash mode input locking, ESC cancellation, and removed timeout
- Fixed bash mode process group spawn/kill for proper cleanup
- Fixed bash mode Ctrl+C interrupt handling
- Fixed toolset switching to be atomic (prevents tool desync race)
- Fixed hooks config state to use settings as source of truth
- Fixed @ file selection during search debounce
- Fixed 5MB image size limit with progressive compression
- Fixed invalid tool call ID recovery
- Fixed stale queued approvals after successful approval flow
- Fixed Skill tool isolated blocks in conversation context
- Fixed messages starting with `/` to be sent to agent when unknown command
- Fixed auto-update ENOTEMPTY errors with cleanup and retry

## 0.13.6

- Added image reading support to Read tool (PNG, JPG, GIF, WEBP, BMP files are visually displayed)
- Added shell alias expansion in bash mode (sources from `.zshrc`, `.bashrc`, etc.)
- Added query prefill support for `/search` command (`/search [query]`)
- Added arrow key navigation for tab switching in `/models`
- Improved Skill tool output with more explicit success messages
- Added automatic retry for 409 “conversation busy” errors
- Added message restoration to input field after queue errors
- Fixed agent name consistency using single source of truth
- Fixed `/clear` command output message to clarify messages are moved to history
- Fixed streaming flicker with aggressive static content promotion
- Fixed cursor position placed at end when navigating command history
- Fixed ADE links to work in tmux
- Reduced image resize limit to 2000px for multi-image requests
- Fixed queue-cancel hang and stuck queue issues
- Fixed premature cancellation of server-side tools in mixed execution

## 0.13.5

- Added automatic image resizing for clipboard paste (images larger than 2048x2048 are resized to fit API limits)
- Improved error feedback when image paste fails
- Fixed conversation ID being passed correctly to resume data retrieval

## 0.13.4

**Default startup behavior reverted to single-threaded experience.** Based on user feedback, `letta` (with no flags) now resumes the agent’s “default” conversation instead of creating a new conversation each time.

| Command                         | 0.13.0 - 0.13.3                    | 0.13.4+                     |
| ------------------------------- | ---------------------------------- | --------------------------- |
| `letta`                         | Creates new conversation each time | Uses “default” conversation |
| `letta --new`                   | Error (was deprecated)             | Creates a new conversation  |
| `letta --continue` (no session) | Silently creates new               | Errors with helpful message |

- Changed `letta` (no flags) to resume the “default” conversation with message history
- Repurposed `--new` flag to create a new conversation (for users who want concurrent sessions)
- Changed `--continue` fallback to error with helpful suggestions instead of silently creating new

## 0.13.3

- Added `messaging-agents` bundled skill for sending messages to other agents
- Added ability to deploy existing agents as subagents via the Task tool
- Fixed interrupt handling race condition when tool approvals are in flight

## 0.13.2

- Added skills frontmatter pre-loading for subagents (skills defined in subagent configs are auto-loaded)
- Added output truncation for Task tool to prevent context overflow
- Added auto-cleanup for overflow files
- Fixed auto-allowed tool execution tracking for proper interrupt handling
- Fixed hardcoded embedding model (now uses server default)

## 0.13.1

- Added `--default` flag to access agent’s default conversation (alias for `--conv default`)
- Added `--conv <agent-id>` shorthand (e.g., `letta --conv agent-xyz` → uses that agent’s default conversation)
- Added default conversation to `/resume` selector (appears at top of list)
- Added `working-in-parallel` bundled skill for coordinating parallel subagent tasks
- Added conversation resume hint in exit stats
- Improved startup performance with reduced time-to-boot
- Fixed stale approvals being auto-cancelled on session resume
- Fixed auth type display on startup
- Fixed memory block retrieval for `/memory` command

## 0.13.0

**Where did my old conversation go?** If you upgraded from an earlier version and your previous messages seem missing, don’t worry! Your messages are in the agent’s **default conversation**. Just run `letta --agent <your-agent-id> --default` to access them.

This release introduces **Conversations** - a major change to how Letta Code manages chat sessions. Your agent can now have many parallel conversations, each contributing to its learning, memory, and shared history.

### What Changed

**Before 0.13.0:**

- Each agent had a single conversation
- Starting Letta Code resumed the same conversation
- `/clear` reset the agent’s context window

**After 0.13.0 (updated in 0.13.4):**

- Each startup resumes the **default conversation** (reverted from 0.13.0-0.13.3 behavior)
- Your agent’s **memory is shared** across all conversations
- `/new` creates a new conversation (for parallel sessions)
- `/clear` clears in-context messages
- Use `/resume` to browse and switch between past conversations
- Use `letta --new` to create a new conversation for concurrent sessions

### Migration Guide

If you’re upgrading from an earlier version, you may notice that starting Letta Code puts you in a **new conversation** instead of continuing where you left off. Here’s what happened:

**Your old messages still exist!** They’re in your agent’s **default conversation** - the original message history before conversations were introduced. You can find it at the top of the `/resume` selector, or access it directly with the commands below.

**Easiest way to access them (0.13.1+):**

Terminal window

```
# Use the --default flag with your agent name
letta -n "Your Agent Name" --default


# Or with agent ID
letta --agent <your-agent-id> --default


# Or use the shorthand (agent ID only)
letta --conv <your-agent-id>
```

The default conversation also appears at the top of the `/resume` selector.

**Alternative methods:**

1. **View them on the web** at `https://platform.letta.com/agents/<your-agent-id>`

2. **Have your agent recall them** using one of these prompts:

   **Using the `recall` subagent:**

   ```
   Can you use the recall subagent to find our most recent messages? I'd like to continue where we left off.
   ```

   **Using the `conversation_search` tool:**

   ```
   Can you use conversation_search to find our most recent messages so we can continue where we left off?
   ```

   **Using the `searching-messages` skill:**

   ```
   Can you load the searching-messages skill and use it to find our most recent messages?
   ```

3. **Export and reference your agent file** by running `/export` (saves to `<agent-id>.af`), then ask your agent:

   ```
   I downloaded my agent file to ./agent-xxxx.af - can you read it and look through the "messages" array to find our most recent conversation?
   ```

Going forward, all new conversations will be accessible via `/resume`, and the default conversation is always available via `--default`.

### Full Changelog

- Added Conversations support - each session creates an isolated conversation while sharing agent memory
- Added `/resume` command to browse and switch between past conversations
- Added `--resume` (`-r`) and `--continue` (`-c`) flags to resume last session
- Added `--conversation` (`-C`, `--conv`) flag to resume a specific conversation by ID
- Added default agents (Memo and Incognito) auto-created for new users
- Changed `/clear` to start a new conversation (non-destructive) instead of deleting messages (reverted in 0.13.4)
- Fixed Task tool rendering issues with parallel subagents
- Fixed ADE links to include conversation context

## 0.12.7

- Fixed text wrapping in collapsed bash output display
- Renamed `memory-defrag` skill to `defragmenting-memory` to follow naming conventions
- Added automatic retry for transient network errors during LLM streaming
- Improved plan mode flexibility for writing plan files

## 0.12.6

- Added `memory` subagent for cleaning up and reorganizing memory blocks
- Added `defragmenting-memory` built-in skill with backup/restore workflow
- Added streaming output display for long-running bash commands
- Added line count summary for Read tool results
- Added network retry for transient LLM streaming errors
- Added Skill tool support in plan mode (load/unload/refresh are read-only)
- Fixed tool approval flow that was broken by ESC handling changes
- Improved Task tool and subagent display rendering
- Fixed UI flickering in Ghostty terminal

## 0.12.5

- Added terminal title and progress indicator for approval screens
- Added `LETTA_DEBUG_TIMINGS` environment variable for request timing diagnostics
- Fixed “Create new agent” from selector being stuck in a loop

## 0.12.4

- Fixed subagent display spacing and extra newlines
- Fixed subagent live streaming not updating during execution

## 0.12.3

- Added LSP diagnostics to Read tool for TypeScript and Python files
- Added `refresh` command to Task tool for rescanning custom subagents
- Added file-based overflow for long tool outputs
- Fixed left/right arrow key cursor navigation in approval text inputs
- Fixed pre-stream approval desync errors with keep-alive recovery
- Fixed subagents not inheriting parent’s tool permission rules

## 0.12.2

- Added `/ralph` and `/yolo-ralph` commands for autonomous agentic loop mode
- Fixed read-only subagents (explore, plan, recall) to work in plan mode
- Fixed Windows PowerShell ENOENT errors with shell fallback

## 0.12.1

- Added `recall` subagent for searching parent agent’s conversation history
- Fixed agent selector not showing when LRU agent retrieval fails
- Fixed approval desync issues for slash commands and queued messages
- Fixed SDK retry race conditions on streaming requests
- Fixed pending approval denials not being cached on ESC interrupt
- Fixed stale processConversation calls affecting UI state after interrupts

## 0.12.0

- Refactored to use new client-side tool calling via the messages endpoint
- Added `acquiring-skills` skill for discovering and installing skills from external repositories
- Added `migrating-memory` skill for copying memory blocks between agents
- Updated skills system (migrating-memory, finding-agents, searching-messages)
- Improved interrupt handling with better messaging
- Fixed ESC interrupt to properly stop streams
- Fixed skill scripts to work when installed via npm
- Fixed Task tool (subagent) rendering issues
- Fixed bash mode exit behavior after submitting commands
- Fixed binary file detection being overly aggressive
- Fixed approval results handling when auto-handling remaining approvals
- Fixed stream retry behavior after interrupts

## 0.11.1

- Added system prompt and memory block configuration for headless mode
- Added `--input-format stream-json` flag for programmatic input handling
- Improved parallel tool call approval UI

## 0.11.0

- Added inline dialogs for improved user experience
- Improved token counter display
- Fixed server-side tools incorrectly showing as interrupted

## 0.10.5

- Fixed Windows installation issues
- Fixed keyboard shortcuts for Ctrl+C, Ctrl+V, and Shift+Enter

## 0.10.4

- Fixed iTerm2 keybindings
- Fixed ESC and CTRL-C handling across all dialogs

## 0.10.3

- Added desktop notifications when UI needs user attention
- Added read-only shell commands support in plan mode

## 0.10.2

- Added Ctrl+V support for clipboard image paste in all terminals
- Fixed keybindings
- Fixed model name display in welcome screen

## 0.10.1

- Added Shift+Enter multi-line input support

## 0.10.0

- Added visual diffs for Edit/Write tool returns
- Added automatic retry for transient LLM API errors
- Added custom slash commands support (`/commands`)
- Added scrolling and manual ordering to command autocomplete
- Added toggle to show all agents in `/agents` view
- Added per-resource queues for parallel tool execution
- Fixed plan mode on non-default toolsets
- Fixed CLI crash when browser auto-open fails in WSL

## 0.8.0

- Added GLM-4.7 model support
- Added `/new` command for creating new agents
- Added `/feedback` command improvements
- Added memory reminders to improve memory usage
- Renamed `/resume` to `/agents` (with backwards-compatible alias)
- Fixed plan mode path resolution on Windows

## 0.7.4

- Added support for bundled skills and multi-source skill discovery
- Increased loaded\_skills block limit to 100k characters

## 0.7.3

- Added support for Claude Pro and Max plans
- Added optional telemetry
- Added `--system` flag for existing agents
- Fixed Windows-specific issues

## 0.7.2

- Added `/help` command with interactive dialog
- Added `/mcp` command for MCP server management
- Added `/compact` command for message compaction
- Added text search for all models
- Improved memory tool visibility with colored name and diff output

## 0.7.1

- Added BYOK (Bring Your Own Key) support - use your own API keys
- Added `/usage` command to check usage and credits
- Added `--info` flag to show project and agent info
- Added naming dialog when pinning agents

## 0.7.0

- Added `/memory` command to view agent memory blocks
- Added ‘add-model’ skill for adding new LLM models
- Added Gemini 3 Flash model support
- Added feedback UI

## 0.6.3

- Added support for relative paths in all tools
- Added tab completion for slash commands
- Added Kimi K2 Thinking model
- Added personalized thinking prompts with agent name
- Added goodbye message on exit
- Renamed `/bashes` to `/bg`

## 0.6.2

- Added stateless subagents via Task tool
- Added Kimi K2 Thinking model support
- Improved subagents UI

## 0.6.1

- Added autocomplete for slash commands
- Faster startup with cached tool initialization
- Added `exit` and `quit` as aliases for `/exit`

## 0.6.0

- Added profile-based persistence with startup selector
- Added `/profile` command for managing profiles
- Added simplified welcome screen design
- Added double Ctrl+C to exit from approval screen
- Added paginated agent list in `/resume`
- Added `/description` command to update agent description
- Added message search

## 0.5.2

- Added `/resume` command with improved agent selector UI
- Added `LETTA_DEBUG` environment variable for debug logging
- Added agent description support
- Added GPT-5.2 support
- Added Gemini 3 (Vertex) support

## 0.5.1

- Added startup status messages showing agent info

## 0.5.0

- Added `/init` command for initializing memory blocks
- Added system prompt swapping
- Changed default naming to PascalCase

## 0.4.1

- Added `/download` command to export agent file locally
- Added Skills omni-tool

## 0.4.0

- Added Claude Opus 4.5 support
- Added toolset switching UI
- Added `--toolset` flag
- Added Gemini tools support
- Added model-based toolset switching
- Added eager cancel functionality

## 0.3.0

- Added sleeptime memory management
- Added `--sleeptime` CLI flag
- Added GPT-5.1 models support
- Added Gemini-3 models support
- Added `--fresh-blocks` flag for isolation
- Added `/swap` command for model switching

## 0.2.0

- Added `/link` and `/unlink` commands for managing agent tools
- Added Skills support
- Added parallel tool calling
- Added multi-device sign in support
- Added agent renaming capability

## 0.1.16

- Added Sonnet 4.5 with 180k context window

## 0.1.15

- Added multiline input support
- Added `--new` flag for creating new memory blocks
- Added agent URL display in commands

## 0.1.11

- Added Claude Haiku 4.5 to model selector
- Added project-level agent persistence with auto-resume
- Added API key caching
- Added `--model` flag
- Added GLM-4.6 support
- Added autocomplete for commands
- Added up/down for history navigation
- Added `fetch_web` to default tool list

## 0.1.10

- Added `stream-json` output format

## 0.1.9

- Added pretty preview for file listings in approval dialog
- Added `LETTA_BASE_URL` environment variable support

## 0.1.8

- Added usage tracking
- Added ESC to cancel operations
- Added Ctrl-C exit with agent state dump

## 0.1.3

- Initial release of Letta Code, the memory-first coding agent
