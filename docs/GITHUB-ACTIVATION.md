# Activate DeepSeek Harness from GitHub (keyless-first)

This fork is in developer preview. Use a private Codespace for an interactive agent. The smoke workflow proves only that the CLI can start its local Web UI; GitHub Actions does **not** persist a Web UI after the job finishes.

## Check GitHub Actions smoke

- Workflow: `.github/workflows/dsh-github-activation-smoke.yml`
- Trigger: push on `feature/dsh-github-activation-20261105` when the workflow file changes.
- Runner: GitHub-hosted `ubuntu-latest` + Node 24.
- Pinned CLI: `@deepseek-ai/dsh@0.2.2-rc.1`.
- Safety: loopback-only Web UI on 127.0.0.1:3080, no model calls, no API credentials or public deployment. Telemetry disabled for this job.
- Pass means that the npm CLI and HTTP listener started. It does not mean agent inference succeeded.

## Use the Web UI in GitHub Codespaces (private)

1. Open this repository's **Code > Codespaces** menu and create a Codespace from this feature branch, if your GitHub plan offers a free Codespaces allowance.
2. In its terminal run:

   ```sh
   node --version
   npx --yes @deepseek-ai/dsh@0.2.2-rc.1 web --no-open --port 3080
   ```

3. Use the exact private launch URL printed by the CLI. In Codespaces **Ports**, forward 3080 with **Private** visibility only. Do not publish the launch token, open the port to everyone, or put credentials into git.
4. Select a separate, disposable workspace. Configure a provider in the UI only after verifying its cost. A model/provider is needed for real AI work; this smoke test does not provide one.

If Codespaces is unavailable or out of free quota, use the same command on a Windows machine with Node 24.9+ and launch the local URL shown by DSH. Keep terminal open.

No paid API, public deploy, merge, or GitHub permission change is authorized by this guide.
