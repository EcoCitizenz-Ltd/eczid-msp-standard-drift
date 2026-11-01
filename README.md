# ECZ-ID MSP Standard Drift

Compare a customer repository's current machine-trust projection with an MSP-approved baseline without making a universal trust or compliance verdict.

This is a thin GitHub Marketplace discovery wrapper over the already-tested ECZ-ID MSP engine. It delegates to immutable engine commit `fedb5cb7633e7cf74c952291a7fbe302e5333af6`; it does not duplicate the engine or create a second source of truth.

## Quick start

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
