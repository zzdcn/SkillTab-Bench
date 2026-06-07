# SkillTab-Bench

This repository contains the code and benchmark resources for **SkillTab-Bench: Benchmarking Skill-Driven Agents for Multi-Turn Industrial Table Analysis**.

## Environment Setup

SkillTab-Bench requires a Python environment with the Nanobot runtime available. The examples below use Bash.

```bash
git clone <repo-url>
cd SkillTab-Bench

python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
```

Install Nanobot in the same environment. If Nanobot is available as a local source repository, install it in editable mode:

```bash
python -m pip install -e path/to/nanobot
```

Configure the model provider before running the benchmark. By default, the runner reads provider and model settings from:

```text
$HOME/.nanobot/config.json
```

You may also pass another configuration file with `--base-config`.

## Run Examples

All commands below should be executed from the repository root.

List available task ids:

```bash
python isolated_benchmark_runner/run_isolated_task.py --list-tasks
```

Prepare benchmark workspaces without calling the model:

```bash
python isolated_benchmark_runner/run_isolated_task.py --skill-mode both --run-id exp_001
```

Run one task with skills enabled:

```bash
python isolated_benchmark_runner/run_isolated_task.py \
  --task-id task_gaokao_shandong_2025_recommendation \
  --skill-mode on \
  --run-id exp_001 \
  --execute
```

Run the same task with skills disabled:

```bash
python isolated_benchmark_runner/run_isolated_task.py \
  --task-id task_gaokao_shandong_2025_recommendation \
  --skill-mode off \
  --run-id exp_001 \
  --execute
```

Run selected tasks with both skill settings:

```bash
python isolated_benchmark_runner/run_isolated_task.py \
  --task-id task_company_weekly_order_risk,task_company_weekly_sales_performance \
  --skill-mode both \
  --run-id exp_001 \
  --execute
```

Run all tasks:

```bash
python isolated_benchmark_runner/run_isolated_task.py \
  --all-tasks \
  --skill-mode both \
  --run-id exp_001 \
  --execute
```

Use a custom provider configuration:

```bash
python isolated_benchmark_runner/run_isolated_task.py \
  --task-id task_gaokao_shandong_2025_recommendation \
  --skill-mode on \
  --run-id exp_001 \
  --base-config path/to/config.json \
  --execute
```

Evaluate one completed run:

```bash
python isolated_benchmark_runner/evaluate_task_outputs.py \
  --run-root runs/task_gaokao_shandong_2025_recommendation/skill_on/exp_001
```

Evaluate both skill settings for all tasks in a run:

```bash
python isolated_benchmark_runner/evaluate_task_outputs.py \
  --run-id exp_001 \
  --skill-mode both \
  --all-tasks
```

Use a specific judge provider and model:

```bash
python isolated_benchmark_runner/evaluate_task_outputs.py \
  --run-root runs/task_gaokao_shandong_2025_recommendation/skill_on/exp_001 \
  --judge-config path/to/config.json \
  --judge-provider <provider-name> \
  --judge-model <model-name>
```
