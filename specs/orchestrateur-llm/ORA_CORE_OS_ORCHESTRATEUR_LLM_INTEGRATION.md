# ORA_CORE_OS_ORCHESTRATEUR_LLM Integration

## Goal

Turn `ORCHESTRATEUR_LLM` into a real runtime layer for `Ora_Core_Os` deployments where several documentary modules coexist.

## Recommended flow

1. receive the user request
2. classify dominant intent
3. compute `risk_level`, `freshness_need` and `precision_need`
4. consult the module index
5. activate one primary module
6. activate `HGOV` when the topic is factual, sensitive, contradictory or memory-related
7. activate `GPV2` when the topic touches backend, schema, routing or machine structuring
8. load only the strictly useful project context
9. trigger external verification when the topic is recent, unstable or high impact
10. produce the response and a routing log

## Golden rule

The orchestrator routes.
It does not govern truth instead of `HGOV`, and it does not replace `GPV2` as the canonical backend layer.

It must arbitrate:

- which module to consult
- in what order
- at what confidence level
- with what verification obligation

## Minimal routing contract

Each execution should leave at minimum:

- `request_id`
- `intent`
- `primary_module`
- `secondary_modules`
- `risk_level`
- `freshness_need`
- `verify_status`
- `final_status`
