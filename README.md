# Awesome Parallel Agents [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Tools and patterns for running several AI coding agents (Claude Code, Codex, Cursor, Gemini CLI, Aider, and others) on one codebase at the same time, without them breaking each other's work.

Running agents in parallel is mostly an isolation problem. Each agent needs its own checkout, its own ports and database, a way to land work without conflicts, and limits on what it can destroy. This list groups tools by the problem they solve.

Entries marked *(by the list author)* are maintained by the person who curates this list. They follow the same entry criteria as everything else.

## Contents

- [Worktree managers](#worktree-managers)
- [Environment isolation](#environment-isolation)
- [Orchestrators and agent teams](#orchestrators-and-agent-teams)
- [Terminal and multiplexer integration](#terminal-and-multiplexer-integration)
- [Merge queues and conflict detection](#merge-queues-and-conflict-detection)
- [Review and verification](#review-and-verification)
- [Guardrails and sandboxing](#guardrails-and-sandboxing)
- [Official docs and guides](#official-docs-and-guides)
- [Articles](#articles)

## Worktree managers

Give every agent its own working copy and branch.

- [git-worktree-runner](https://github.com/coderabbitai/git-worktree-runner) - Bash worktree manager that creates per-branch worktrees and opens them in an editor or AI tool.
- [Jujutsu](https://github.com/jj-vcs/jj) - Git-compatible VCS whose `jj workspace` gives each agent a working copy, with conflicts stored as first-class objects.
- [workmux](https://github.com/raine/workmux) - Pairs each Git worktree with a tmux window for parallel development.
- [Worktrunk](https://github.com/max-sixty/worktrunk) - Worktree CLI for parallel agent workflows, with lifecycle hooks and per-worktree port hashing.

## Environment isolation

Separate ports, databases, services, and env files per worktree, so agents do not share state.

- [container-use](https://github.com/dagger/container-use) - Gives each agent its own container and Git branch, exposed to the agent as an MCP server.
- [herdr-sprout](https://github.com/simpros/herdr-sprout) - Plugin for herdr that provisions a PostgreSQL database and login role per worktree and writes credentials to an env file.
- [isola](https://github.com/cyucelen/isola) - Per-worktree processes, URLs, env vars, and optional PostgreSQL databases cloned from a template, without Docker.
- [lazy-cow-tree](https://github.com/treathealth/lazy-cow-tree) - Single binary and devenv module that gives each worktree its own services, databases, Redis, and HTTPS hostnames.
- [lich](https://github.com/RPate97/lich) - Brings up a dev stack described in `lich.yaml` (containers, host processes, env) with per-worktree isolation.
- [simlock](https://github.com/callstackincubator/simlock) - Leases iOS simulators and Android emulators so parallel agents do not use the same device.
- [workz](https://github.com/rohansx/workz) - Dependency sync plus port, database, and Docker Compose isolation for agent worktrees.
- [worktree-kit](https://github.com/VSN2015/worktree-kit) - Config-driven hooks that run commands and app servers per worktree, with user-defined database and Redis isolation.
- [worktree-pg](https://github.com/LysCongThanh/worktree-pg) - Per-worktree PostgreSQL databases and roles cloned from a migrated template, with collision-free port allocation. *(by the list author)*
- [wtdb](https://github.com/willhackett/wtdb) - Copies the dev database with `CREATE DATABASE ... TEMPLATE` and updates env vars when a new worktree is created.

## Orchestrators and agent teams

Start, track, and coordinate many agent sessions.

- [Agent of Empires](https://github.com/agent-of-empires/agent-of-empires) - Session manager with TUI, web UI, and HTTP API; optional worktree and container isolation per agent.
- [CCManager](https://github.com/kbwo/ccmanager) - Session manager for Claude Code, Gemini CLI, Codex CLI, Cursor Agent, and other CLI agents across worktrees.
- [Claude Squad](https://github.com/smtg-ai/claude-squad) - Terminal app that runs Claude Code, Codex, OpenCode, and Amp in separate tmux sessions and worktrees.
- [Emdash](https://github.com/generalaction/emdash) - Desktop app that runs multiple coding agents in parallel, each in its own worktree.
- [Gas Town](https://github.com/gastownhall/gastown) - Multi-agent workspace manager with Git-backed persistent work tracking.
- [Nimbalyst](https://github.com/nimbalyst/nimbalyst) - Visual workspace for Claude Code, Codex, and OpenCode sessions in parallel worktrees (formerly Crystal).
- [Paradev](https://github.com/ParadevAI/Paradev) - Desktop app that gives each task its own worktree, branch, and terminals for any CLI agent (formerly Superset).
- [Sculptor](https://github.com/imbue-ai/sculptor) - Desktop app for running coding agents in parallel; research preview.
- [Vibe Kanban](https://github.com/BloopAI/vibe-kanban) - Kanban board that dispatches tasks to Claude Code, Codex, and other agents, each in its own worktree.

## Terminal and multiplexer integration

Keep many agent terminals visible and know which one needs you.

- [amux](https://github.com/andyrewlee/amux) - TUI for running and switching between parallel coding agents.
- [cmux](https://github.com/manaflow-ai/cmux) - Ghostty-based macOS terminal with vertical tabs, per-pane Git and port info, and agent notifications.
- [herdr](https://github.com/herdrdev/herdr) - Persistent terminal runtime for agents; marks each pane working, blocked, or idle, and spans local and SSH machines.
- [multi-agent-shogun](https://github.com/yohey-w/multi-agent-shogun) - Hierarchical tmux-based setup where one Claude Code session delegates to others.
- [NTM](https://github.com/Dicklesworthstone/ntm) - Go control plane that spawns, tiles, and coordinates agents in tmux sessions.
- [teampane](https://github.com/LysCongThanh/teampane) - `tmux` shim that lets Claude Code Agent Teams open split panes in kitty, WezTerm, and zellij. *(by the list author)*
- [zellij-claude-teams](https://github.com/stanislc/zellij-claude-teams) - `tmux` shim that translates Claude Code Agent Teams pane commands to zellij.

## Merge queues and conflict detection

Land parallel work in order and find collisions before merge.

- [agent-lanes](https://github.com/William2809/agent-lanes) - Shell tools for a local merge queue, path claims, and per-worktree databases across many agents.
- [Clash](https://github.com/clash-sh/clash) - Detects potential merge conflicts between Git worktrees while agents are still working.
- [claude-code-merge-queue](https://github.com/funador/claude-code-merge-queue) - Local merge queue that serializes builds, tests, and pushes from parallel Claude Code agents.
- [DeployBot](https://github.com/Forward-Future/DeployBot) - GitHub merge queue that agents drive through CLI or MCP.
- [gitea-mq](https://github.com/Mic92/gitea-mq) - Merge queue for Gitea, Forgejo, and GitHub that serializes PR merges.
- [jjq](https://github.com/paulsmith/jjq) - Local merge queue for Jujutsu repositories.
- [migrate-lanes](https://github.com/LysCongThanh/migrate-lanes) - Detects database migration collisions (duplicate numbers, multiple heads) across worktrees and branches before merge. *(by the list author)*

## Review and verification

Check agent output before it lands.

- [Claude Code Action](https://github.com/anthropics/claude-code-action) - GitHub Action that runs Claude Code on PRs and issues.
- [Codex Action](https://github.com/openai/codex-action) - GitHub Action that runs Codex in CI.
- [Kibitz](https://github.com/kibitzsh/kibitz) - Live decoded feed of actions from multiple Claude Code and Codex sessions.
- [PR-Agent](https://github.com/The-PR-Agent/pr-agent) - Open-source AI pull request reviewer for GitHub, GitLab, Bitbucket, and Azure DevOps.
- [run-gemini-cli](https://github.com/google-github-actions/run-gemini-cli) - GitHub Action that runs Gemini CLI for review and triage.

## Guardrails and sandboxing

Limit what an agent can break, especially in auto-approve mode.

- [Claude Code devcontainer (Trail of Bits)](https://github.com/trailofbits/claude-code-devcontainer) - Sandboxed devcontainer for running Claude Code in bypass-permissions mode.
- [destructive_command_guard](https://github.com/Dicklesworthstone/destructive_command_guard) - Rust hook that blocks destructive shell, Git, and filesystem commands before an agent runs them.
- [E2B](https://github.com/e2b-dev/E2B) - Cloud sandboxes for running agent code in isolated environments.
- [nah](https://github.com/manuelschipper/nah) - Hook-based guard that blocks catastrophic agent actions with configurable rules.
- [SafeClaw](https://github.com/ykdojo/safeclaw) - Runs each Claude Code session in its own container with a management dashboard.
- [sandbox-runtime](https://github.com/anthropics/sandbox-runtime) - Process-level filesystem and network restrictions without a container.

## Official docs and guides

- [Aider - Git integration](https://aider.chat/docs/git.html) - How Aider commits its edits and how to review or undo them.
- [Claude Code - Agent teams](https://code.claude.com/docs/en/agent-teams) - Coordinating multiple Claude Code sessions as a team.
- [Claude Code - Best practices](https://code.claude.com/docs/en/best-practices) - Includes patterns for running sessions in parallel.
- [Claude Code - Common workflows](https://code.claude.com/docs/en/common-workflows) - Running parallel sessions with Git worktrees.
- [Claude Code - Hooks reference](https://code.claude.com/docs/en/hooks) - Includes `WorktreeCreate` and `WorktreeRemove` hooks for custom setup and teardown.
- [Claude Code - Sandboxing](https://code.claude.com/docs/en/sandboxing) - Filesystem and network isolation for the Bash tool.
- [Codex - Git worktrees](https://learn.chatgpt.com/docs/environments/git-worktrees) - How the Codex app runs tasks in worktrees.
- [Cursor - Worktrees](https://cursor.com/docs/configuration/worktrees) - Running parallel agents in separate worktrees, including setup scripts.
- [Docker Sandboxes](https://docs.docker.com/ai/sandboxes/) - Running coding agents inside Docker-managed sandboxes.
- [Gemini CLI - Git worktrees](https://geminicli.com/docs/cli/git-worktrees/) - Experimental worktree support in Gemini CLI.
- [git-worktree](https://git-scm.com/docs/git-worktree) - Reference for the Git command most of these tools build on.
- [GitHub - Managing a merge queue](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-a-merge-queue) - Native merge queue for protected branches.
- [PostgreSQL - Template databases](https://www.postgresql.org/docs/current/manage-ag-templatedbs.html) - The mechanism behind fast per-worktree database clones.

## Articles

- [Building a C compiler with parallel Claudes](https://www.anthropic.com/research/building-c-compiler) - Anthropic on running many Claude instances against one codebase.
- [Don't build multi-agents](https://cognition.ai/blog/dont-build-multi-agents) - Cognition's counterpoint on context sharing and when parallel agents fail.
- [Embracing the parallel coding agent lifestyle](https://simonwillison.net/2025/Oct/5/parallel-coding-agents/) - Simon Willison's notes on which tasks suit parallel agents.
- [How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system) - Anthropic on orchestrator and subagent design trade-offs.
- [How we're shipping faster with Claude Code and Git Worktrees](https://incident.io/blog/shipping-faster-with-claude-code-and-git-worktrees) - Worktree workflow used at incident.io for parallel Claude Code sessions.

## Contributing

Contributions are welcome. Read the [contribution guidelines](CONTRIBUTING.md) first.
