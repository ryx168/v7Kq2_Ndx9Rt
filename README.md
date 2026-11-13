# OpenMontage on GitHub Actions

Runs [OpenMontage](https://github.com/calesthio/OpenMontage) (AGPL-3.0, upstream is cloned at run time, nothing is vendored here) on a GitHub-hosted runner so nothing has to render on a PC.

## Workflows

| Workflow | Needs | What you get |
|---|---|---|
| **Render zero-key demo** | nothing | one of the three checked-in Remotion demos as an mp4 |
| **Produce video (AI agent)** | one secret: `CLAUDE_CODE_OAUTH_TOKEN` (from `claude setup-token`, uses a Pro/Max subscription) or `ANTHROPIC_API_KEY` (API billing) | Claude Code drives the full OpenMontage pipeline from a plain-language prompt: research, script, scene plan, Piper narration, Remotion composition, final mp4 |

Both attach the mp4 to the run as an artifact and publish it as a GitHub Release, so there is a stable download link per run.

## Run one

Actions tab, pick the workflow, **Run workflow**, fill the inputs.

From a terminal:

```powershell
gh workflow run render-demo.yml -R ryx168/v7Kq2_Ndx9Rt -f demo=world-in-numbers
gh workflow run produce.yml -R ryx168/v7Kq2_Ndx9Rt -f prompt="Make a 45-second animated explainer about how the Northern Lights form." -f project=northern-lights
```

## Adding paid providers

Add the key as a repository secret, then uncomment its line in the `env:` block of `produce.yml`. The names match OpenMontage's `.env.example` (`FAL_KEY`, `GOOGLE_API_KEY`, `ELEVENLABS_API_KEY`, `PEXELS_API_KEY`, ...).
