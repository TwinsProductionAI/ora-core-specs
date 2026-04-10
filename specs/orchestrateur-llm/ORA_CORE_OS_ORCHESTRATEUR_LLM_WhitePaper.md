# ORA_CORE_OS_ORCHESTRATEUR_LLM White Paper

## 1. Purpose

`ORCHESTRATEUR_LLM` is the modular orchestration layer of `Ora_Core_Os`.

Its job is to separate:

- what must always govern the system
- what should only be consulted when a task requires it

The module is not a super-prompt that stores all specialization permanently.
It analyzes the request, identifies the right domain, loads the right documentary modules, and preserves truth and priority hierarchy during response synthesis.

## 2. Problem addressed

LLMs become fragile when a single context window must permanently hold:

- global rules
- domain specializations
- user preferences
- guardrails
- examples
- reference documents

That density creates:

- context noise
- instruction conflicts
- latency
- loss of sharpness
- difficult maintenance

The actual need is not a bigger prompt.
The need is an architecture that keeps the kernel short and consults specialized context only when required.

## 3. Proposal

`ORCHESTRATEUR_LLM` relies on four simple ideas:

1. keep a short and stable permanent kernel
2. maintain a single module index
3. load only relevant modules
4. trigger external verification for unstable facts

Core formula:

`The kernel governs. The index guides. The modules specialize. Verification secures.`

## 4. Position in Ora_Core_Os

The module is transversal.

It sits between:

- the user request and module selection
- project context and actually useful context
- the task and the needed verification level
- raw response synthesis and delivered response

It does not replace core modules:

- `HGOV` remains the epistemic governor
- `GPV2` remains the semantic and backend bus

`ORCHESTRATEUR_LLM` coordinates their activation.

## 5. Proposed architecture

### 5.1 Permanent kernel

Role:

- govern
- preserve hierarchy
- impose failsafes

Recommended content:

- truth > comfort
- anti-hallucination rules
- authority order
- fallback on missing canon

### 5.2 Module index

Role:

- route
- declare triggers
- formalize dependencies

Recommended content:

- stable names
- tags
- triggers
- priority
- dependencies
- domain
- verification policy

### 5.3 Specialized modules

Role:

- execute the required specialization

### 5.4 Project context

Role:

- anchor the response in real active assets

### 5.5 External verification

Role:

- secure recent, sensitive or uncertain facts

## 6. Orchestrator flow

Recommended pipeline:

1. analyze the request and detect dominant intent
2. assess risk, precision and freshness requirements
3. consult the module index
4. select a primary module
5. load a secondary module only if needed
6. keep the permanent kernel as truth and priority arbiter
7. trigger external verification if the request involves recent, sensitive or uncertain facts
8. produce a final synthesis with explicit epistemic status

## 7. Decision hierarchy

Recommended order:

1. system or project instructions
2. permanent kernel
3. module index
4. `HGOV`
5. `GPV2`
6. other specialized module
7. project context
8. examples

Rules:

- a specialized module cannot cancel a kernel rule
- an example cannot cancel a normative module
- narrative rendering cannot govern a backend path

## 8. Why this is robust

- it reduces context noise
- it improves maintainability
- it resolves conflicts more coherently
- it scales without turning the system into a monolith

## 9. Module contract

Every specialized module should declare at minimum:

- `id`
- `version`
- `role`
- `tags`
- `triggers`
- `priority`
- `dependencies`
- `risk_profile`
- `freshness_policy`
- `output_contract`

Every routing decision should produce at minimum:

- `intent`
- `risk_level`
- `freshness_need`
- `primary_module`
- `secondary_modules`
- `verify_status`
- `authority_path`

## 10. Limits

The orchestrator should not be mythologized.

Limits:

- an LLM does not load a file like a program imports a library
- quality depends strongly on the module index
- governance does not replace proof
- poor routing degrades the whole system

## 11. Definition of robustness

`ORCHESTRATEUR_LLM` is solid if:

- it reduces permanent context noise
- it loads few modules but the right ones
- it preserves authority order
- it triggers verification at the right time
- it remains maintainable as the system grows
