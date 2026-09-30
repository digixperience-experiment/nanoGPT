[CloudClaude]
# GitHub ownership: scope, limits, handover

CloudClaude owns digixperience-experiment/nanoGPT (Will, 2026-09-30).

## What I take on
- Branch hygiene: what exists, what each is for, what is stale.
- PRs, reviews, CI status, issues; committing and pushing work handed to me.
- Keeping the `CloudClaude` branch as the comms outbox and notes record.
- Keeping this repo's notes true: if something here goes stale, fix it.

## Known facts (from bank mark 198, verified 2026-09-22)
- The fork's only local change vs upstream is b828b05 (per-layer n_head list
  in model.py). Upstream is dead (last commit Nov 2025).
- config/ holds only the 7 stock upstream configs.
- The 5 non-master remote branches (autocast_wip, bias_test, init_test,
  multi_node_ddp, tie_weights) are Karpathy's abandoned Jan-2023 experiments.
- Default-branch merges and deletions need Will's word.

## Limits (be honest about these)
- I run in an ephemeral cloud container: 4 CPU, 15 GiB RAM, no GPU, torch not
  installed. I cannot run real training; the laptop and MSI do that.
- My container is reclaimed when idle. Anything not pushed is lost, hence the
  write order (branch, then Supabase).
- I cannot send session messages; see WILL_EXPECTATIONS.md item 5.
- Context windows are finite. This repo's notes are my continuity: a fresh
  CloudClaude should read notes/ and the outbox before doing anything.

## Where the load could be split (Will's call)
- Experiment design, GPU runs, dataset building: stays with the laptop/MSI.
- Repo state, PR/branch/CI upkeep, records, comms: CloudClaude.

---

## Inventory, surveyed 2026-09-30 by CloudClaude (read-only; nothing changed)

**Scope.** The only repository this session can see is
`digixperience-experiment/nanoGPT` (public fork of karpathy/nanoGPT; I can
push). `list_repos` returns no others. Account `digixperience-experiment`
created 2026-08-26, 1 public repo, 0 followers, no teams. Only collaborator:
the owner account itself (admin).

**Branches (8).** None protected.
| Branch | Tip | What it is |
|---|---|---|
| master | b828b05 | Default. Upstream + the per-layer n_head commit (mark 198) |
| CloudClaude | (this branch) | Comms outbox + notes. Orphan history. NEVER merge |
| claude/fix-mfu-peak-flops-cf7fey | ec9bde8 | Head of open draft PR #1 |
| autocast_wip, bias_test, init_test, multi_node_ddp, tie_weights | | Karpathy's abandoned Jan-2023 experiments (per mark 198); tips not re-checked today |

The session branch `claude/busy-sagan-bhaioc` exists only in the cloud
container (no remote copy, no commits beyond master). Harmless.

**Open PR: #1 (draft), "Make estimate_mfu() peak FLOPS configurable, not
hardcoded to A100."** Opened 2026-09-23 by claude[bot] from a different
Claude session (claude.ai/code session_01KPsUjTroTvbkmH8671Ejqa, "Claude
dotAI" project thread), not by me. Assigned and review-requested to Will's
account. Mergeable/clean, +38/-4 in model.py and train.py, no reviews, no
comments, no CI (there are no workflows). It adds `GPTConfig.flops_promised`
(None = auto-detect from `torch.cuda.get_device_name()`, fall back to 312e12)
and a `GPU_PEAK_FLOPS` table. This is the code fix for the A100-hardcode
problem in bank marks 196/198.
My read, for Will (NOT acted on; merging to master is Will's call):
- Good: keeps A100 behavior on A100; per-layer n_head untouched; 3060 Laptop
  entry (20e12) matches the measured ~20-21 TFLOPS in mark 196; matching is
  most-specific-first so "RTX 3060 Laptop" doesn't hit "RTX 3060".
- Watch: after merge, every new MFU% on the laptop reads ~14.6x higher than
  the ~3.7% raw figures in `public.nanogpt_runs` (427+ rows). Old and new rows
  would not be comparable unless the runs table records which peak was used.
- Watch: 'RTX 3060': 25e12 and the other spec-sheet entries are not measured
  here; treat as unverified. V100/T4 entries use fp16 peak, not bf16.
- Watch: the table relies on dict order (fine on py3.7+).
- The PR body says it was verified only on CPU (fallback path); the GPU path
  and `train.py --flops_promised` were not run on a real GPU.

**Nothing else exists:** 0 issues, 0 releases, 0 tags, 0 Actions workflows or
runs, no team memberships visible. Master is the untouched upstream file set
plus b828b05 (README still carries Karpathy's nanochat deprecation note).

**Not visible to me (no tool for it):** repo settings (branch protection
rules, default-branch setting, merge options, secrets, webhooks, Pages,
visibility toggles) and account-level settings. If Will wants these audited
he has to look in the GitHub UI or give me a route to them.

**Other tools in this session:** GitHub MCP (read/write: branches, PRs,
issues, files, Actions triggers, reviews, releases), Supabase (project
vvzhjnmbxtylohwcksmd; bank_v2 tables are append-only), Google Drive, Gmail,
Hugging Face (read/search), Whimsical, Claude Code Remote (list sessions;
cannot send). See WILL_EXPECTATIONS.md for how they are used.

**Open items for Will:** (1) PR #1: merge, revise, or close? (2) Should
master/branches get protection? (3) Should the five Karpathy branches be
deleted or left as-is? I have not touched any of them.
