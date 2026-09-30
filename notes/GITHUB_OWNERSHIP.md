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
