# Prompt Efficiently for claude-code

Release candidate. Local host installation verified; see the exact remaining acceptance checks below. Explicit rough input-token estimates and conservative prompt tightening. Not automatic agent metering. Same PE account, free quota and Pro entitlement as the website. No prompt text is sent to PE.

## Prerequisites and setup
Desktop, Python 3.10+, a secure OS credential store, and this folder. In your own terminal create a virtual environment and install the bundled requirements:

    python3 -m venv .venv
    .venv/bin/python -m pip install -r requirements.txt
    .venv/bin/python pe.py login

On Windows use `.venv\Scripts\python.exe`. On Linux a functioning Secret Service keyring is required; no insecure fallback is supported. Dependency downloads need internet. Python keyring is free software, not a paid service.

The email code is entered in your terminal only. Never paste it into Claude/Codex. Sessions use the OS credential store. Run `pe.py logout` to revoke. `pe.py status` checks quota/Pro. `pe.py upgrade` opens the PE website, where you sign in separately.

## Use
The helper reads only stdin, never your workspace. Pipe a prompt from your own trusted tool to `.venv/bin/python pe.py estimate` or `tighten`. Review suggestions before using them. A quota check can consume one free check even if the network drops after acceptance. New helper calls are new uses. Network/auth failures stop instead of bypassing the quota.

## Claude Code plugin
Start a session with `claude --plugin-dir /absolute/path/to/this-folder`. The skill is `pe`; explicitly ask PE to check supplied prompt text. Configure the helper Python environment with its absolute path in your own session. Do not put credentials in project settings. This does not silently intercept Claude requests.

## Limits and release gate
Rough word-based input tokens only, no output/context/tool cost or subscription-credit estimate.



## Local catalog install
After downloading and unzipping, run `claude plugin marketplace add /absolute/path/to/this-folder`, then `claude plugin install prompt-efficiently@prompt-efficiently`. The catalog is bundled locally and no online directory approval is required. An online hosted catalog needs a reachable artifact source, not this relative local path.

Licence: MIT (see LICENSE). Sign-in, rewrites and billing run on Prompt Efficiently servers and are not part of this repository. Not affiliated with the AI products it supports.
