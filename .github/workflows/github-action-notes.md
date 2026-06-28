# Day 41 - GitHub Actions Notes

## 1. Matrix Build Workflow
Purpose: Run same job on multiple Python versions.

```yaml
name: Matrix Build

on:
  push:

jobs:
  matrix-job:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        python-version: [3.10, 3.11, 3.12]

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}

      - run: python --version
````

---

## 2. Manual Workflow (workflow_dispatch)

Purpose: Run workflow manually with input.

```yaml id="p9xq3m"
name: Manual Workflow

on:
  workflow_dispatch:
    inputs:
      environment:
        description: Enter environment
        required: true
        default: staging

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Print Environment
        run: echo "Environment: ${{ github.event.inputs.environment }}"
```

---

## 3. Basic First Workflow

Purpose: Learn basic GitHub Actions steps.

```yaml id="k2q8lm"
name: First Workflow

on:
  push:

jobs:
  greet:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - run: echo "Hello DevOps"

      - run: date

      - run: echo ${{ github.ref_name }}

      - run: ls -la

      - run: echo $RUNNER_OS
```

---

## 4. Pull Request Check Workflow

Purpose: Run checks before merging PR.

```yaml id="t6v1zn"
name: PR Check

on:
  pull_request:
    branches:
      - main

jobs:
  check-pr:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Checking PR from branch: ${{ github.head_ref }}"
```

---

## 5. Scheduled Workflow (Cron Job)

Purpose: Run workflow automatically on schedule.

```yaml id="s3m8qp"
name: Schedule Workflow

on:
  schedule:
    - cron: '19 10 * * *'

jobs:
  backup-job:
    runs-on: ubuntu-latest

    steps:
      - run: echo "Scheduled workflow running"
```

---

# Summary (Very Important)

* push → automatic run
* workflow_dispatch → manual run
* pull_request → PR check
* schedule → time-based run
* matrix → multiple versions testing
