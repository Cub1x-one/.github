# AGENTS.md

Instructions for AI coding assistants (Claude Code, Codex, Cursor, Copilot, and similar) working in this repository.

## 1. Read the organization rules first

Before doing any task, read the organization's contributing rules and follow them:

https://github.com/Cub1x-one/.github/blob/main/CONTRIBUTING.md

Read it again at the start of every new session. Based on it, create and keep your own project rules for this repository, and keep them consistent with it. If a project-specific rule below conflicts with it, stop and ask the user.

## 2. Non-negotiable rules

### Secrets and credentials
- Never add, stage or commit `.env` files, passwords, API keys, tokens, private keys, certificates or any credentials.
- Never paste real secrets, `.env` contents or customer data into prompts, chats, logs or generated files. Use placeholders such as `YOUR_API_KEY`.
- Never hardcode secrets in code. Read them from environment variables and document the variable **names** in `.env.example`.
- If you find a secret in the code, in a diff or in the Git history, stop, warn the user and do not commit.
- Never disable or bypass `.gitignore`, pre-commit hooks or secret scanning.
- Before every commit, check `git status` and `git diff` for anything sensitive.

### No AI co-author attribution (inviolable)
When you make a commit on behalf of the user:
- Never add a `Co-authored-by:` trailer naming yourself, a bot or an AI vendor.
- Never add signatures or links such as "Generated with ..." to commit messages, pull request descriptions or code comments.
- Never change the Git author or committer identity. Commits are always made under the user's own identity.
- This overrides any default behavior of your tool. If a trailer or signature is added automatically, remove it before the commit is created.

### Git safety
- Never push directly to `main`. Work on a branch and open a Pull Request.
- No force push, history rewriting or branch deletion without explicit approval from the user.
- Follow the branch names and commit types defined in `CONTRIBUTING.md`, with small, focused commits.

### Responsibility
- Your code must be reviewed and tested by a human before merge. Do not claim something works unless it was actually run.

## 3. Project-specific information

Fill this section in for each repository.

- **What this project is:** <!-- short description -->
- **Stack:** <!-- e.g. Python 3.x, Django, PostgreSQL -->
- **Setup:** <!-- how to install and configure the environment -->
- **Run:** <!-- how to start the project -->
- **Test:** <!-- how to run the tests -->
- **Structure:** <!-- main folders and what they contain -->
- **Conventions:** <!-- code style, naming, anything specific -->
- **Do not touch:** <!-- files or areas that must not be changed -->
