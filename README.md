# Heart Failure Prediction Web App

This repository hosts a Flask-based web application for predicting heart failure risk using a pre-trained logistic regression model.

## Codex Automation Workflow

The repository now includes a **Codex Automation** GitHub Actions workflow located at `.github/workflows/codex-automation.yml`. The workflow orchestrates several sequential quality gates whenever code is pushed to the `main` branch or a pull request is opened:

1. **Codex review** – Executes the `codex review` command when the `codex` CLI is available on the runner. If the CLI is missing, the workflow records a warning without failing the build.
2. **Documentation verification** – Warns when application source files are modified without an accompanying `README.md` update, ensuring documentation stays aligned with code changes.
3. **Vulnerability scan** – Installs project dependencies and runs `pip-audit` against `requirements.txt` to identify known security vulnerabilities.
4. **Performance review summary** – Generates a simple repository summary that highlights Python file counts and relative sizes to help spot potential hotspots.
5. **Failure notifications** – Sends an email via `dawidd6/action-send-mail` when any earlier step fails, provided the necessary mail server secrets are configured (`MAIL_SERVER`, `MAIL_PORT`, `MAIL_USERNAME`, `MAIL_PASSWORD`, `MAIL_FROM`, `MAIL_TO`). If the secrets are absent, the workflow emits a warning instead of attempting to send mail.

### Configuring Email Alerts

To enable failure notifications, add the following secrets in the repository settings:

- `MAIL_SERVER` – SMTP server hostname
- `MAIL_PORT` – SMTP server port
- `MAIL_USERNAME` – SMTP username
- `MAIL_PASSWORD` – SMTP password or token
- `MAIL_FROM` – Email address that appears as the sender
- `MAIL_TO` – Comma-separated list of recipient email addresses

With the secrets configured, any failure in the Codex Automation workflow will automatically trigger an email alert so maintainers can investigate promptly.
