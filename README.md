# fledge-plugin-roast

Roast a commit through whatever LLM you've configured via [`fledge ai use`](https://github.com/CorvidLabs/fledge). For entertainment purposes only.

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

```bash
fledge roast --severity gentle      # kindly retired engineer
fledge roast --severity harsh       # tired senior dev (default)
fledge roast --severity brutal      # bitter 30-year veteran
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

This plugin is ~100 lines of bash that builds a prompt and pipes it to `fledge ask --no-spec-index "$PROMPT"`. That's it. All the LLM plumbing — provider selection, model fallback, timeouts, env-var precedence — comes from `fledge ask` for free.

## Caveats

- The diff is truncated to 800 lines to keep cloud-model token usage sane. Roasting a 10K-line commit will only see the first 800 lines.
- `fledge ask` needs a working AI provider. Run `fledge doctor` if the AI section isn't green.
- The roast is generated content. Don't quote it in production code review.

## License

MIT
