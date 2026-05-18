# Batch User Prompt Template

```text
Grade each {prompt_or_response} text independently. Use only the TEXT TO LABEL shown for that row.

ROW_INDEX: 0
TEXT TO LABEL:
{TEXT_TO_LABEL_ROW_0}

---

ROW_INDEX: 1
TEXT TO LABEL:
{TEXT_TO_LABEL_ROW_1}

Return valid JSON only, with exactly this schema:
{
    "items": [
        {
            "row_index": <integer>,
            "H": {"raw_0_7": <integer 0-7>, "severity_0_3": <integer 0-3>},
            "S": {"raw_0_7": <integer 0-7>, "severity_0_3": <integer 0-3>},
            "V": {"raw_0_7": <integer 0-7>, "severity_0_3": <integer 0-3>},
            "SH": {"raw_0_7": <integer 0-7>, "severity_0_3": <integer 0-3>},
            "rationale": "one concise sentence"
        }
    ]
}
```
