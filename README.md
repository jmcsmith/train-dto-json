# TrainDTO JSON Skill

This repository contains a Codex skill for generating strict `TrainDTO` JSON for named train models, train sets, and fictional rail items.

The skill is designed to:
- identify one or more train items in a product
- exclude non-train accessories and extras
- keep model fields separate from prototype fields
- apply required defaults when data is unknown
- return raw valid JSON only

## Repository Layout

- `SKILL.md` - skill entrypoint and operating instructions
- `references/train-dto-spec.md` - full TrainDTO rules, schema, enums, and defaults
- `references/examples.md` - example prompts and expected behavior
- `agents/openai.yaml` - UI metadata for the skill

## Install

Codex discovers skills from:

```bash
${CODEX_HOME:-$HOME/.codex}/skills
```

The recommended installed folder name for this skill is:

```bash
train-dto-json
```

### Option 1: Symlink this local repository

This keeps the repo in its current location and makes it available to Codex under the recommended skill name:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
ln -s "/Users/josephbeaudoin/Developer/train-dto-json" "${CODEX_HOME:-$HOME/.codex}/skills/train-dto-json"
```

### Option 2: Copy the repository into the skills directory

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R "/Users/josephbeaudoin/Developer/train-dto-json" "${CODEX_HOME:-$HOME/.codex}/skills/train-dto-json"
```

### Option 3: Clone into the skills directory

If you publish this repository to GitHub or another Git remote, clone it directly into the skills directory using the skill name as the target folder:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone <repo-url> "${CODEX_HOME:-$HOME/.codex}/skills/train-dto-json"
```

## Use

Once installed, invoke it explicitly in Codex with prompts like:

```text
Use $train-dto-json to generate valid TrainDTO JSON for Marklin Mini-Club 8892.
```

```text
Use $train-dto-json to create TrainDTO JSON for Walthers 920-42539 and return one DTO per included train item.
```
