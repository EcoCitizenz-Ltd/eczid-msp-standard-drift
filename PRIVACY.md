# Privacy

This Marketplace wrapper delegates to an immutable ECZ-ID MSP Action in the caller's GitHub Actions workspace. Repository source, report contents, prompts, credentials, secret values and customer evidence are not uploaded to ECZ-ID by the wrapper. There is no hidden telemetry.

An optional client-id is recorded only in the local generated report by the underlying Action. Do not put secrets or regulated data in workflow inputs. GitHub processes workflow logs and artifacts according to the repository's GitHub settings.
