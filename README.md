# Detection Engineering

Detection rules written in Sigma, translated to platform-specific formats,
tested, and validated automatically on every commit.

## How this repository works

Sigma is the single source of truth. Platform-specific rules are generated
from it. Changing a detection means changing the Sigma rule and regenerating
the rest — never editing a translation directly.

## Structure

Each detection lives in its own folder under `detections/`, named by its
MITRE ATT&CK technique ID:

- `rule.yml` — the Sigma rule (source of truth)
- `wazuh.xml` — Wazuh translation
- `sentinel.kql` — Microsoft Sentinel / Defender translation
- `tests/positive.json` — an event that MUST trigger the rule
- `tests/negative.json` — an event that must NOT trigger the rule
- `README.md` — why this detection exists, expected volume, tuning notes

## Detection lifecycle

Every detection here follows seven stages: requirements, research, develop,
test, deploy, tune, retire.

1. **Requirements** — the behaviour to catch, and what an analyst does when it fires
2. **Research** — confirm the telemetry exists and carries the fields needed
3. **Develop** — write logic against the behaviour, not the tool
4. **Test** — prove it fires on the attack AND stays quiet on benign activity
5. **Deploy** — reviewed and merged through a pull request
6. **Tune** — adjusted on evidence from production
7. **Retire** — removed when the behaviour is blocked at source or precision stays poor

## Validation

Every push runs `sigma check` against all rules via GitHub Actions.
A rule that fails validation cannot be merged.

## Current detections

| Technique | Name | Status |
|---|---|---|
| T1053.005 | Scheduled Task Persistence | experimental |
| T1003.001 | LSASS Credential Dumping | experimental |
| T1047 | WMI Process Creation | experimental |