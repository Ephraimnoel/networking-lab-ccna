# Lab 05 — Troubleshooting Deliberate Faults

**Status: Planned**

## Objective

Practice a structured troubleshooting process by introducing and investigating three controlled configuration faults after the baseline network works.

## Scenario

A support technician receives reports that some users cannot communicate. The technician must gather evidence, isolate the fault, correct it, and verify the result.

## Prerequisites

- Baseline network completed and evidence saved
- A clean backup of the working `.pkt` file exists
- [`docs/troubleshooting-log.md`](../docs/troubleshooting-log.md) reviewed

## Tasks to perform

1. Save a known-good copy before changing anything.
2. Introduce only one planned fault at a time.
3. Record the observed symptom without assuming the cause.
4. Form an initial hypothesis.
5. Run appropriate show commands and connectivity tests.
6. Record evidence and identify the root cause.
7. Apply a correction and verify the result.
8. Restore or preserve the final intended configuration.
9. Repeat for the remaining two faults.

## Planned faults

- Fault #1: incorrect VLAN assignment on an endpoint access port.
- Fault #2: incorrect or incomplete trunk configuration.
- Fault #3: incorrect host IP address or default gateway.

These faults are planned scenarios, not completed incidents. Their symptoms and outcomes must be filled in only after you perform them.

## Commands/concepts to investigate

- `show vlan brief`
- `show interfaces trunk`
- `show interfaces status`
- `show ip interface brief`
- `show ip route`
- `ping`
- `traceroute`
- OSI-layer isolation and hypothesis-driven troubleshooting

## Expected outcome

You should produce three evidence-backed investigation records. Do not assume that the expected fault is the actual root cause until tests support it.

## Evidence to capture

- Pre-fault baseline
- Symptom or failed test
- Diagnostic commands and outputs
- Corrective change
- Post-correction verification
- Completed troubleshooting record

## Completion criteria

- All three faults were introduced personally after baseline validation.
- Each fault has a complete investigation record.
- Root cause is supported by evidence.
- Corrective action and verification are documented.
