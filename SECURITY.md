# Security Policy

Gem is an experimental AI personal assistant that answers inbound phone calls on behalf of its author. It runs as a Telnyx AI Assistant on a live telephone number and will, in time, act on the author's Gmail and Google Calendar accounts. This document explains what counts as a security issue for the project, how to report one privately, and how the project handles credentials and personal data.

## Reporting a Vulnerability

Please report security issues **privately**. Do not open a public issue or pull request that describes the problem.

Use GitHub's private vulnerability reporting: [Report a vulnerability](https://github.com/rohingosling/gem/security/advisories/new). The report is visible only to the maintainer until a fix and an advisory are published.

A useful report includes: a description of the issue and its impact; the file, commit, or endpoint affected; steps to reproduce; and a proof of concept if you have one.

This is a single-maintainer, experimental project. You can expect an acknowledgement within 7 days and a fix on a best-effort basis; you will be credited in the advisory if you wish.

## Responsible Testing

Gem is reachable on a real telephone number and speaks to real callers. **Do not test against the live assistant** — do not call the number to probe it, attempt prompt injection during a call, or try to make the assistant disclose information or take actions — without written permission from the maintainer. Test against the code and configuration published in this repository instead.

## Scope

| In scope | Out of scope |
|----------|--------------|
| Anything in this repository that would expose a credential, a personal detail, or a way to act on the maintainer's Telnyx, Gmail, or Google Calendar accounts. | Vulnerabilities in Telnyx or Google services themselves — report those to the vendor. |
| The integration service, once published: authentication of incoming webhook calls, handling of OAuth tokens, validation of tool arguments, and logging of call data. | Denial of service by calling the number repeatedly, and social engineering of the maintainer. |
| Weaknesses in the published prompts or tool definitions that would let a caller extract data or trigger actions they should not. | Automated scanner output without a demonstrated impact. |

## Supported Versions

Only the `main` branch is maintained. There are no tagged releases yet; fixes land on `main`.

## How the Project Handles Credentials and Personal Data

- **No credential is ever committed.** Telnyx API keys, and in future Google OAuth client secrets and tokens, are kept outside version control and are ignored by git before they can be staged.
- **The public repository is a curated subset.** The assistant's prompts, test recordings, and credentials are held privately. Publication is driven by an explicit include list, so a file is published only if it is named for publication, and the published tree is reviewed before every push.
- **GitHub secret scanning and push protection are enabled** on this repository, so a push containing a recognised credential format is rejected.
- **Exposure is treated as compromise.** If a credential is ever found in this repository or its history, it is revoked and replaced immediately and the exposure is recorded in an advisory.
- **Personal data stays out of the public tree.** The assistant's knowledge — contact numbers, availability, and other details it uses on calls — is deliberately not published.
- **Least privilege for integrations.** The integration service will request only the Google API scopes it needs (sending mail, managing calendar events), will verify that incoming webhook requests originate from Telnyx, and will not log call content beyond what is needed to deliver a message.
