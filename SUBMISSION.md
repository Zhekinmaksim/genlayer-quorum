# Quorum portal submission

## Category

Builder > Intelligent Contracts

## Title

Quorum

## Contribution date

October 19, 2026 (publication and live verification).

## Description and notes

```text
Quorum is a GenLayer contract for a weighted evidence threshold. A claimant fixes the claim, evidence texts, weights and threshold; a distinct assessor countersigns their commitment before evaluation. The contract calls gl.nondet.exec_prompt inside gl.eq_principle.prompt_comparative. Validators independently judge each supplied item's textual support and compare the accept vector and terms hash. This contract's own non-deterministic judgment controls the stored accept mask, accepted weight and MET/NOT_MET outcome. Input commitments, strict integer bits and terminal settlement are enforced; the result hash binds all decision fields. Three Studio cases finalized with SUCCESS and MAJORITY_AGREE: exact threshold, below threshold despite a rejected high-weight item, and no supporting items. All used two distinct signing accounts. Ten local regression groups and SDK validation pass. Assessment concerns supplied text; it does not authenticate evidence or verify external facts.
```

984 characters.

## Primary evidence links

- Source repository: https://github.com/Zhekinmaksim/genlayer-quorum
- Studio contract: https://explorer-studio.genlayer.com/address/0xE5902271f340375ec58BA8E29eb6DA22716492e9

## Additional evidence

- Exact deployed source: https://github.com/Zhekinmaksim/genlayer-quorum/blob/6a7ac888b22bf91ae65ecb98c519f1971b2bd0bd/contract.py
- Deployment: https://explorer-studio.genlayer.com/tx/0x80b63044a3599b6f403f3ca96dbd5578220670d3a68cb55873aec68c769106c9
- quorum-exact-001: https://explorer-studio.genlayer.com/tx/0x64eb420dfebc35836e68d058dcd8d6b9237d748044e63977ee75a4a5c217fd74
- quorum-below-001: https://explorer-studio.genlayer.com/tx/0x1ab2a9fbf4a025a87d0203e8851f012d9836d41e6a2b735a2152381ad4b5da01
- quorum-none-001: https://explorer-studio.genlayer.com/tx/0xd0251427b7f24853baa8a3ab1901de0b60fbd2d37ea1d4ca86935ba158872a28
- Inputs, outputs and countersign transactions: https://github.com/Zhekinmaksim/genlayer-quorum/blob/main/evidence.json

## Verification

10/10 local regression groups and SDK semantic validation passed. Each of the
three live cases matched the expected stored result. Deployment, countersigns
and evaluations are FINALIZED, execution SUCCESS, consensus MAJORITY_AGREE.
Normal consensus was used (leader_only=false).

Two distinct existing accounts were used for creator and counterparty; both are
controlled by the same tester. This verifies role separation. Local tests mock
SDK/model behavior and use SHA3-256 as a hash stub; live execution uses the actual
SDK Keccak256.

## Submission status

Ready for manual form entry. No portal form was created or sent.
Studio is a test environment. Portal acceptance is not guaranteed.
