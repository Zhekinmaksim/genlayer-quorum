# Quorum verification

Executed on October 19, 2026. Exact inputs and transactions are in evidence.json.

## Local checks

10 groups passed: all eight 3-bit outcomes, countersign authorization and wrong
hashes, countersign prerequisite, terminal settlement, strict vectors, malformed
consensus payloads, independent mock judgments and disagreement, input integrity
before model calls, immutable inputs and result commitment coverage. Hash stubs
use SHA3-256; live execution uses SDK Keccak256. Tests reject Address.ZERO usage.

## Executed live cases

- quorum-exact-001: expected {"outcome":1,"accepted_weight":5,"accept_mask":3}; observed match; FINALIZED/SUCCESS/MAJORITY_AGREE.
- quorum-below-001: expected {"outcome":2,"accepted_weight":5,"accept_mask":3}; observed match; FINALIZED/SUCCESS/MAJORITY_AGREE.
- quorum-none-001: expected {"outcome":2,"accepted_weight":0,"accept_mask":0}; observed match; FINALIZED/SUCCESS/MAJORITY_AGREE.

Each case was created by the creator account and countersigned by a distinct
counterparty before evaluation. Both accounts share one test operator.

## Additional test ideas

Prompt-injection variants and malicious counterparty behavior require broader
adversarial evaluation. No live injection-resistance proof is claimed.
