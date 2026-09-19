# Troubleshooting Log

**Status: Template — no faults have been introduced or fixed yet**

After the baseline network works, introduce each fault yourself, save the pre-fault state, and complete one investigation record per fault. Do not describe a planned fault as an actual incident until you have performed it.

## Planned fault scenarios

1. **Incorrect VLAN assignment:** place an endpoint on the wrong access VLAN.
2. **Incorrect trunk configuration:** remove or alter a required trunk setting.
3. **Incorrect IP/default gateway:** give an endpoint an invalid address or gateway.

## Investigation template

### Fault #__ — [short title]

- **Status:** Planned
- **Date performed:** To be completed
- **Affected device/endpoint:** To be completed
- **Intended fault:** To be completed after introduction

#### Symptom

_To be completed from observed behavior. Do not write the expected symptom as if it was observed._

#### Initial hypothesis

_To be completed before running diagnostic tests._

#### Commands/tests performed

| Order | Command or test | Reason | Actual result |
|---:|---|---|---|
| 1 | To be completed | To be completed | To be completed |

#### Evidence

_Add sanitized screenshots, command output, or test references only after performing the investigation._

#### Root cause

_To be completed after evidence supports the conclusion._

#### Corrective action

_To be completed after applying the correction._

#### Verification

_Record the actual retest, result, and evidence reference. Do not claim success in advance._

#### Lessons learned

_To be completed after the investigation._

## Troubleshooting principles

- Start with the symptom and scope.
- Form a hypothesis before changing configuration.
- Change one relevant thing at a time where possible.
- Preserve useful before-and-after evidence.
- Verify both the correction and the absence of unintended effects.
