# Quorum

Assesses the textual support of each evidence item, then sums the agreed weights of accepted items against a countersigned threshold.

Published and verified on October 19, 2026.
[Deployed Studio contract](https://explorer-studio.genlayer.com/address/0xE5902271f340375ec58BA8E29eb6DA22716492e9).
[Submission text and links](SUBMISSION.md).

## Material nondeterminism

The contract runs its own `gl.nondet.exec_prompt` judgment inside
`gl.eq_principle.prompt_comparative`. Validators independently repeat that
judgment; the wrapper compares the decision vector and input commitments.
The accepted vector determines the stored outcome. The comparator is LLM-based;
the contract revalidates integer bits, shape and hashes after it returns.
See [GenLayer equivalence documentation](https://docs.genlayer.com/developers/intelligent-contracts/equivalence-principle).

## Agreed terms and immutable inputs

A claimant fixes the claim, evidence texts, weights and threshold at creation. A distinct assessor address must countersign the terms hash before evaluation. Weights express the parties' policy, not model-estimated probabilities. Identical evidence is rejected, but semantic overlap or coordinated parties can still bias the policy.

Stored input commitments are recomputed before model calls. Model decisions must
be integer 0/1 values with the exact vector length; booleans and floats are rejected.
Every stored settlement, including UNDETERMINED, is terminal. The result hash
binds input commitments, roles, outcome, decision fields and reason.


## API

- `open_claim(id, assessor, claim_text, item_texts, item_weights, threshold)` -> terms hash
- `countersign(id, terms_hash)` -> designated assessor only
- `evaluate(id)` -> permissionless, after countersigning
- `get_terms_hash(id)` -> commitment for the assessor
- `get_result(id)` -> JSON hashes, roles, reason, accept mask, accepted weight and threshold
- `get_outcome(id)` -> 0 pending, 1 MET, 2 NOT_MET, 3 UNDETERMINED

The constructor takes no arguments. Views return ordinary values or JSON strings.
Storage containers are declared by annotation and never manually constructed.
The runtime dependency is pinned. See [schema.json](schema.json) for the ABI.

## Executed verification

- SDK semantic validation, lint and ABI extraction passed with genvm-linter 0.11.0.
- 10 local regression groups passed, including all eight 3-bit decision vectors,
  countersign permissions, malformed results, commitments and terminal execution.
- Three live Studio cases matched expected results. Deployment, countersigns and
  evaluations finalized with SUCCESS and MAJORITY_AGREE, leader_only=false.
- Creator and counterparty used distinct addresses under the same test operator.

[evidence.json](evidence.json) records exact inputs, source commit/SHA-256,
transactions and stored outputs; [smoke.json](smoke.json) contains the cases.
Run local checks with `python3 sim/check.py`. Local SDK/model behavior is mocked,
including a SHA3-256 hash stub. Live execution uses the actual SDK Keccak256.
ABI validation checks storage and method types; it does not execute GenVM.

## Limits

This is assessment of supplied text. External facts, signatures, authorship and
source authenticity are not verified. Models can agree incorrectly. JSON framing
does not guarantee prompt-injection resistance. A network consensus failure may
leave a transaction unaccepted rather than store UNDETERMINED. There is no
external security audit or guaranteed portal acceptance. Studio is a test
environment; no mainnet deployment or portal submission is claimed.

## Publication correction

A preliminary deployment exposed an unsupported Address.ZERO constant. The
published revision constructs the zero address explicitly. All passing live
cases above use the corrected deployment. Evidence records the superseded address.
