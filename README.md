# ECZ-ID MSP Standard Drift

Compare a customer repository's current machine-trust projection with an MSP-approved baseline without making a universal trust or compliance verdict.

**Start without an ECZ-ID account or API key.** GitHub Actions runner usage follows your GitHub plan.

This is a thin GitHub Marketplace discovery wrapper over the already-tested ECZ-ID MSP engine. It delegates to immutable engine commit `fedb5cb7633e7cf74c952291a7fbe302e5333af6`; it does not duplicate the engine or create a second source of truth.

## Run it now

Create `.github/workflows/eczid-msp.yml`, paste this complete first-run workflow, commit it, then run it from the **Actions** tab.

```yaml
name: ECZ-ID MSP Standard Drift

on:
  workflow_dispatch:

permissions:
  contents: read

jobs:
  eczid:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        uses: actions/checkout@v7

      - uses: EcoCitizenz-Ltd/eczid-msp-standard-drift@v1
        with:
          mode: propose
```

### First-run path

1. Add the workflow above.
2. Run it manually with **Run workflow**.
3. Review the job output and generated local evidence report.
4. Use the bounded outputs below in your own MSP/customer policy.
5. If you want the wider estate view, [run the free MSP / MSSP Machine Trust Check](https://msp.ecocitizenz.com/trust-check?utm_source=github&utm_medium=action-readme&utm_campaign=msp-machine-trust&utm_content=eczid-msp-standard-drift&ecz_source=github&ecz_surface=eczid-msp-standard-drift&intent=msp-machine-trust-check).

## Minimal Action step

Already have a workflow? Add only this step:

```yaml
- uses: EcoCitizenz-Ltd/eczid-msp-standard-drift@v1
```

## Inputs

| Input | Required | Default | Meaning |
|---|---:|---|---|
| `path` | no | `.` | Repository-relative path to inspect. |
| `client-id` | no | empty | Optional MSP/customer identifier included in the proposed/current projection. |
| `baseline` | no | `.eczid/msp-baseline.json` | Repository-relative path to the approved baseline JSON. |
| `output` | no | `eczid-msp-standard-drift.json` | Repository-relative path for the drift report or proposed baseline. |
| `mode` | no | `check` | check or propose. Propose emits a baseline proposal but never commits it. |
| `fail-on` | no | `invalid` | invalid or never. Drift does not fail by default. |

## Outputs

| Output | Meaning |
|---|---|
| `result-state` | NO_CHANGE, CHANGED, BASELINE_PROPOSED, or INVALID_INPUT. |
| `current-hash` | SHA-256 hash of the current normalized projection. |
| `expected-hash` | SHA-256 hash of the approved baseline projection when present. |
| `changed-field-count` | Number of top-level projection fields that differ. |
| `report-path` | Path to the generated drift report or proposed baseline. |
| `next-action-url` | One contextual next step when drift is observed. |

## Trust boundary

- Runs in the caller's GitHub Actions workspace.
- No repository source upload to ECZ-ID.
- No hidden telemetry.
- Missing ECZ-ID identity is neutral and never means unsafe, non-compliant or untrusted.
- No universal safety, trust, certification or compliance verdict.
- No pay-to-pass.
- Local MSP/customer policy decides what observed evidence means.

## Engine provenance

Delegates to `EcoCitizenz-Ltd/eczid-msp-machine-trust-toolkit/actions/standard-drift@fedb5cb7633e7cf74c952291a7fbe302e5333af6`. Marketplace wrapper releases must only advance this pin after the shared engine's cross-platform tests are green.

## Version pinning

Use `@v1` for ECZ-ID's stable compatibility channel. Where your organisation requires immutable third-party Action references, pin the wrapper repository to its full release commit SHA. The wrapper itself always pins the shared MSP engine by full commit SHA.

## Support and policy

See [PRIVACY.md](PRIVACY.md), [SECURITY.md](SECURITY.md), [SUPPORT.md](SUPPORT.md) and [LICENSE.txt](LICENSE.txt).

## Why this wrapper exists

GitHub Marketplace discovery works at the repository root. The underlying MSP engine intentionally keeps related Actions together; this wrapper makes one proven capability independently discoverable without copying implementation or creating maintenance drift.
