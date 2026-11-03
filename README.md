# Poker AI private-study automation

Runs every 15 minutes through GitHub Actions, conditional on repository Secrets being configured. The workflow processes **one subtitle chunk per run** and stores a short analysis JSON plus a checkpoint JSON in a private Google Drive folder. No copyrighted course files or AI outputs are committed to this public repository.

## Required GitHub Actions secrets
- `OPENAI_API_KEY` — OpenAI API key (charged separately from ChatGPT).
- `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `GOOGLE_REFRESH_TOKEN` — Google OAuth credentials with Drive file read/write scope, authorized for the account holding the course.
- `SOURCE_FOLDER_ID` — the user's RYE course folder ID.
- `OUTPUT_FOLDER_ID` — the user's private Poker AI Knowledge Base folder ID.

**Security:** Set secrets in GitHub → Poker → Settings → Secrets and variables → Actions. Never commit them to the repository. The repository is currently public: keep course videos, transcripts, and study outputs **off GitHub**. Refresh tokens require the user to create/authorize an OAuth client and must not be pasted into chat.

Use Actions → Poker AI analysis → Run workflow for a manual test once secrets are configured. Check job logs for errors. A GitHub Actions schedule is best effort and can be delayed or skipped.

The first run does not know which pre-existing *manual* study files are already done. It may perform redundant work unless a baseline completion manifest is imported into Drive. Progress percentages therefore require a separate inventory.

The processor uses a chunk-level checkpoint `auto_state_v1.json` in Drive. It does **not** deliver a complete tournament solver or prove GTO accuracy. Source texts are sent to the configured OpenAI API for analysis.
