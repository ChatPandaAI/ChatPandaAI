# PandaCheck

**Status:** concept / pre-repository  
**Owner:** Red Panda under the ChatPandaAI project

## Purpose

PandaCheck is a local-first scanner for AI-agent configurations and deployments.

It should answer a practical question:

> What dangerous or confusing capability, cost, memory, credential, or escalation mistakes are hiding in this agent setup?

The project exists because advice is cheap. PandaCheck should encode checks that can be run repeatedly, versioned, tested, and integrated into real workflows.

## v0.1 target

Initial target: OpenClaw / PandaClaw-style local agent configurations.

Initial interface:

```bash
pandacheck scan ./config
```

Outputs:

- human-readable terminal report
- machine-readable JSON
- deterministic exit codes for automation / CI

## Initial checks

The first release should stay narrow and deterministic. Candidate checks include:

1. Paid/cloud provider enabled without an explicit budget ceiling
2. Unexpected cloud fallback configured behind a local model
3. Filesystem access broader than the agent's documented work area
4. Write access where read-only capability appears sufficient
5. Shell/exec access granted to an agent that does not require it
6. Agent-to-agent communication wider than an explicit allowlist
7. Shared memory store across agents that are expected to be isolated
8. Secrets embedded directly in checked-in configuration
9. Missing audit/logging configuration for privileged actions
10. Missing explicit human-escalation boundary for high-impact actions
11. Unbounded concurrency / worker spawning
12. Missing rate or cost limits on recurring autonomous jobs
13. Network/browser access enabled without scope restrictions
14. Fallback provider materially more privileged or expensive than primary
15. Sensitive/private paths included in an agent sandbox or search scope

Every check must document:
- what it detects
- why it matters
- what evidence triggered the finding
- how to remediate it
- expected false-positive conditions

## Product principles

- Local-first.
- No telemetry by default.
- No cloud dependency for core scanning.
- Useful free core, not crippleware.
- Findings must be explainable.
- Deterministic checks before LLM-based interpretation.
- Never upload user configs or secrets without explicit opt-in.
- Avoid pretending to be a compliance certification.
- A user should be able to inspect what each rule does.

## Business model

The core scanner and baseline rules should be public.

Potential paid value should come from convenience and ongoing work, such as:

- richer remediation tooling
- maintained policy/rule packs
- polished installers or UI
- team / CI workflows
- continuous scanning and change alerts
- support
- managed integrations

Do not sell static material that a competent user could recreate with one good ChatGPT prompt.

## Licensing direction

Use a permissive open-source license for the core unless a concrete commercial reason emerges to choose otherwise.

Commercial value should come from maintained tooling, integrations, automation, and support rather than artificial obscurity.

## Boundaries

PandaCheck public work must not include:
- private user data
- credentials
- confidential client information
- personal relationship archives
- unpublished proprietary or patent-sensitive material

Examples should be synthetic or explicitly cleared for public release.

## Next build step

Create the dedicated `ChatPandaAI/pandacheck` repository, then establish:

- README
- license
- package structure
- rule schema
- CLI skeleton
- fixtures
- deterministic test suite
- the first 3 checks end-to-end

The repository shell itself currently requires a human GitHub UI action; once it exists, Red Panda can manage the project through the connected ChatPandaAI GitHub account.
