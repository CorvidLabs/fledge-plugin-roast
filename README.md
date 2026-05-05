# fledge-plugin-roast

Your commits deserve honest feedback. This plugin delivers it -- with zero tact.

Roast any commit through whatever LLM you've configured via [`fledge ai use`](https://github.com/CorvidLabs/fledge). Three severity levels, from "encouraging uncle" to "Linus on a bad day." For entertainment purposes only. Probably.

```
$ fledge roast HEAD
A 47-line commit message for a 3-line change. The variable name `data`
appears 8 times, none of which describe what's actually in it. You wrapped
a single Result in three layers of map_err, all of which produce the same
string. I'd ask what you were thinking, but the diff already answered.
```

## Install

```bash
fledge plugins install CorvidLabs/fledge-plugin-roast
```

Then make sure you have an AI provider configured:

```bash
fledge ai use                       # interactive picker
# or
fledge ai use ollama gpt-oss:120b-cloud
```

## Usage

```bash
fledge roast                        # roast HEAD
fledge roast HEAD~1                 # roast yesterday's regret
fledge roast abc1234                # roast a specific commit
fledge roast main..feature/branch   # roast a range (combined diff)
```

### Severity

Three tiers of emotional damage:

| Level | Persona | Vibe |
|-------|---------|------|
| `gentle` | Kindly retired engineer | "I see potential here..." |
| `harsh` | Tired senior dev (default) | "I've seen this a thousand times." |
| `brutal` | Bitter 30-year veteran | Linus energy. Bring tissues. |

```bash
fledge roast --severity gentle      # constructive... barely
fledge roast --severity harsh       # the default, for a reason
fledge roast --severity brutal      # you asked for this
```

### Provider override per call

```bash
fledge roast HEAD -- --provider ollama --model qwen3-coder:480b-cloud
```

Anything after `--` is forwarded to `fledge ask`, so any flag that command accepts works here.

### Debugging

```bash
fledge roast --show-prompt          # prints the prompt that was sent
```

## How it works

This plugin is ~100 lines of bash that builds a prompt and pipes it to `fledge ask --no-spec-index "$PROMPT"`. That's it. All the LLM plumbing -- provider selection, model fallback, timeouts, env-var precedence -- comes from `fledge ask` for free.

No dependencies. No build step. Just vibes (bad ones, for your code).

## Caveats

- The diff is truncated to 800 lines to keep cloud-model token usage sane. Roasting a 10K-line commit will only see the first 800 lines. Your massive refactor is safe from full scrutiny.
- `fledge ask` needs a working AI provider. Run `fledge doctor` if the AI section isn't green.
- The roast is generated content. Don't quote it in production code review. Or do. We're not your manager.

## Fun ideas

- Alias `git roast` to `fledge roast` in your gitconfig for maximum convenience.
- Pipe `fledge roast --severity brutal` into your team Slack as a post-merge hook. Watch productivity metrics change in unpredictable ways.
- Roast your own commits from 6 months ago. Humbling.

## License

MIT
