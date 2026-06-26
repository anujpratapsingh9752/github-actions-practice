# Day 40 - My First GitHub Actions Workflow

## Objective

Learn how to create and run my first GitHub Actions workflow.

---

# What I Did Today

* Created a new GitHub repository.
* Cloned the repository to my local machine.
* Created the `.github/workflows` folder.
* Created my first workflow file (`hello.yml`).
* Triggered the workflow on every push.
* Ran shell commands on a GitHub-hosted Ubuntu runner.
* Used `actions/checkout@v4` to download repository code into the runner.
* Printed the current date.
* Printed the branch name.
* Listed repository files.
* Printed the runner operating system.
* Intentionally broke the workflow using `exit 1`.
* Read the error logs.
* Fixed the workflow and made the pipeline green again.

---

# Repository Structure

```text
.github/
└── workflows/
    └── hello.yml
```

---

# Workflow

```yaml
name: First Workflow

on:
  push:

jobs:
  greet:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Print Hello
        run: echo "Hello DevOps Brother!"

      - name: Current Date
        run: date

      - name: Show Branch Name
        run: echo ${{ github.ref_name }}

      - name: List Repository Files
        run: ls -la

      - name: Show Runner Operating System
        run: echo $RUNNER_OS
```

---

# GitHub Actions Keywords

## name

Display name of the workflow.

---

## on

Defines when the workflow should start.

Example:

```yaml
on:
  push:
```

Runs the workflow whenever code is pushed.

---

## jobs

A workflow is made of one or more jobs.

Example:

```yaml
jobs:
  greet:
```

---

## runs-on

Specifies which runner (machine) will execute the job.

Example:

```yaml
runs-on: ubuntu-latest
```

GitHub creates a fresh Ubuntu virtual machine for the workflow.

---

## steps

A job is divided into multiple sequential steps.

Example:

```yaml
steps:
```

---

## uses

Uses a pre-built GitHub Action.

Example:

```yaml
uses: actions/checkout@v4
```

Downloads (checks out) the repository into the runner.

Without checkout, the runner does not have the project files.

---

## run

Executes shell commands on the runner.

Example:

```yaml
run: echo "Hello"
```

---

# GitHub Context Variable

```yaml
${{ github.ref_name }}
```

Returns the branch name that triggered the workflow.

Example Output:

```text
main
```

---

# Runner Environment Variable

```bash
echo $RUNNER_OS
```

Example Output:

```text
Linux
```

---

# Useful Commands

Print current date

```bash
date
```

List repository files

```bash
ls -la
```

Print message

```bash
echo "Hello DevOps Brother!"
```

---

# Workflow Failure

Intentional failure:

```yaml
- name: Break Workflow
  run: exit 1
```

## Why it failed?

`exit 1` returns a non-zero exit code.

GitHub marks the job as failed.

Common log:

```text
Error: Process completed with exit code 1.
```

---

# Key Learning

* GitHub Actions runs workflows in the cloud.
* Every workflow starts on a fresh runner.
* `actions/checkout@v4` downloads the repository into the runner.
* `run` executes Linux shell commands.
* GitHub provides built-in variables like `${{ github.ref_name }}`.
* Pipelines can be intentionally failed for debugging practice.
* Reading logs is an important DevOps skill.

---

# Interview Revision

**Q. What is GitHub Actions?**

GitHub Actions is a CI/CD automation service that automatically runs workflows when events (such as push or pull request) occur.

---

**Q. What is a Workflow?**

A workflow is a YAML file that defines automated tasks.

---

**Q. What is a Job?**

A job is a group of related steps executed on the same runner.

---

**Q. What is a Step?**

A step is a single task inside a job.

---

**Q. Why do we use actions/checkout?**

To download the repository code into the GitHub runner.

---

**Q. What does run do?**

It executes shell commands on the runner.

---

# Today's Outcome

✅ Created my first GitHub Actions workflow.

✅ Successfully ran a green pipeline.

✅ Understood workflow structure.

✅ Used GitHub variables.

✅ Learned how to debug a failed workflow.

✅ Fixed the pipeline successfully.

