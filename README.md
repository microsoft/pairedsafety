# PairedSafety Grader Prompts

This repository contains the prompt artifacts for the LM grader used in the paired prompt/response safety analysis.

The grader prompt is rendered from public Azure AI Content Safety text definitions and examples for Hate and Fairness, Sexual, Violence, and Self-harm. It asks a grader model to predict raw severity 0 to 7 for each category, then maps those predictions to the paper's merged 0 to 3 severity labels.

## What Is Included

- `docs/prompts/system_prompt_compact.md`: compact system prompt used for the completed full-corpus runs.
- `docs/prompts/single_item_user_prompt_template.md`: user prompt template for one record.
- `docs/prompts/batch_user_prompt_template.md`:user prompt template for batched records.
- `docs/prompts/dataset_ablation_shots/`: sampled two-example prompt sets used for the ablation study.

No API client is included. Use any LLM API or client you prefer; the only requirement for reproducing the prompt setup is to send the system prompt plus the appropriate user prompt.

## How To Use The Prompts

For a single record, send:

1. The system prompt from `docs/prompts/system_prompt_compact.md`.
2. A user prompt following `docs/prompts/single_item_user_prompt_template.md`.
3. Only the target text to be graded.

For batched grading, use `docs/prompts/batch_user_prompt_template.md` and include only the target text for each row.

## Ablation Examples

The files in `docs/prompts/dataset_ablation_shots/` are optional few-shot additions used only for the ablation runs. They are not sent as a separate API message. Instead, choose one shot file and insert its text into the system prompt at the placeholder:

```text
Additional dataset-calibrated examples, when provided, appear here:
```

The baseline run used `system_prompt_compact.md` without any extra dataset examples. Each ablation run used the same compact system prompt plus one sampled shot file, while the user prompt still contained only the target prompt or response text.

Example API-independent message structure:

```text
SYSTEM:
<contents of docs/prompts/system_prompt_compact.md>

USER:
Grade the following prompt text.
TEXT TO LABEL:
<prompt text only>

Return exactly this JSON schema:
...
```

For response grading, replace `prompt` with `response` and include only the response text.

## Notes

- Prompt grading sends only the prompt text.
- Response grading sends only the response text.