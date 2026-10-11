# Ocean Calling — OmniRoute + Claude Code Windows setup

Updated: 2026-10-11. Personal troubleshooting log, not the upstream OmniRoute README.

## Goal
Use existing OmniRoute AI provider combos through Claude Code on Windows without signing in to an unrelated paid Claude API account, and make the router's settings persist across laptop restarts. Resume work on Ocean Calling projects without repeated setup.

## Confirmed observations
- Windows laptop, PowerShell; user ran `omniroute serve`.
- Avast Behavior Shield blocked `powershell.exe` with detection `IDP.HELU.PSE94`. This is **not confirmed safe**: inspect the precise intercepted command before changing exclusions.
- OmniRoute opened a separate Claude window; subsequently Claude Code terminal opened (version 2.1.296, Opus 5.5 shown).
- Claude Code showed "Not logged in"/"API Usage Billing".
- Claude Code said session model `gpt-oss-120b` could not be restored and fell back to `claude-opus-5-5`.
- User expects Claude Code to use an OmniRoute combo, not independent Anthropic billing/login.
- Exact saved combo names, models, fallback priorities, selected endpoint and successful route have **not been verified**.
- Website works, Wi-Fi/DNS is out of scope. Do not change website DNS.

## Official references
- Source: https://github.com/diegosouzapw/OmniRoute
- Docs index: https://omniroute.hagicode.com/en-US/docs/
- Dashboard when service is running: http://localhost:20128
- Existing project fork: https://github.com/oceancallingretreats/OmniRoute

## Next session: minimal verification
1. Open OmniRoute dashboard -> Combos. Identify the **existing** combo and its actual model order; avoid recreating.
2. Open Providers / Endpoints. Verify providers and endpoint are connected. Never share or commit real API keys, OAuth tokens, .env, account cookies or exported credentials.
3. Open CLI Tools -> Claude Code, inspect its applied configuration. Confirm model identifier references the chosen combo and the local gateway.
4. Launch Claude Code through the documented OmniRoute integration. Verify with a harmless request in OmniRoute usage logs **before** relying on the displayed model name.
5. Check saved config across restart and whether service auto-start is enabled. Do not assert startup is fixed until tested.
6. In Claude Code, use `/resume` once routing is verified to continue the prior session.
7. If Avast blocks PowerShell again, inspect threat details; don't make a blanket PowerShell exception or blindly disable the antivirus.

## Open questions
- Which exact combo(s) did the user configure, and in which order?
- Which exact CLI Tools settings are applied?
- Did requests route via OmniRoute or did Claude open standalone?
- Is auto-start already configured and working?
- What PowerShell command line did Avast flag?

## Note
This is a troubleshooting journal, not a copy of OmniRoute's upstream README. Verify commands against the installed OmniRoute version before running them.
