# ORA_CORE_OS_H_NERONS Integration

## Goal

Turn `H-NERONS` into a stable pre-emission factual governance gate for `Ora_Core_Os` deployments.

## Runtime position

`H-NERONS` sits after the model draft and before final user emission.

It should be activated when a response contains verifiable factual claims, especially if the topic is recent, numeric, regulatory, technical or otherwise high impact.

## Recommended flow

1. receive the final draft
2. extract verifiable claims
3. classify each claim by type and freshness sensitivity
4. build a redacted lookup plan
5. inject external evidence from an orchestrator or connector
6. cross-check the draft claims against weighted evidence
7. assign a qualification state for each claim
8. regenerate or bound the response
9. emit GL and GL_G audit traces

## Minimal input contract

Each execution should provide at minimum:

- `META`
- `DRAFT_TEXT`
- `CONTEXT`
- `ROUTING`
- optional `EXTERNAL_EVIDENCE`

`EXTERNAL_EVIDENCE` can come from a live connector, a document set, or a local test bundle.

## Minimal output contract

Each execution should leave at minimum:

- `Claims`
- `LookupPlan`
- `Status`
- `Validation`
- `Packet.GL`
- `Packet.GL_G`
- `RegulatedResponse`

## Qualification states

- `VERIFIED`
- `PARTIALLY_VERIFIED`
- `CONFLICT_DETECTED`
- `UNSURE_EXTERNAL`
- `UNSURE_EXPLICIT`

## Guardrails

- never send private data in outbound query terms
- prioritize primary and official sources when they exist
- block strong claims if verification is insufficient
- expose uncertainty instead of hiding it
- keep the audit trace machine-readable

## Deployment note

The public runtime bundle supports local evidence injection by design.
Live web lookup can be added by an orchestrator or connector without changing the qualification model.
