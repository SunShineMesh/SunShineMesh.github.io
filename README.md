# SunShineMesh.github.io

Visual explainer for **MeshCredit v2** — an on-ledger, multi-dimensional agent trustworthiness certificate (the "passport") on the XRP Ledger, built for SwissHacks 2026 · Ripple Pillar 3 (Agent Financial Infrastructure / Know Your Agent).

- **Live site:** https://sunshinemesh.github.io
- **Code repo:** https://github.com/SunShineMesh/SunShine

---

## What this site is

A static, self-contained site (`index.html` + `deck.html` + `assets/`) that covers the idea, the 6-dimension certificate model, the principal hierarchy, the data flywheel, the XRPL features, and real XRPL testnet results (2026-06-21 run) with live explorer links. `deck.html` is a keyboard-navigable pitch deck (→ / space to advance). The interactive demo runs locally against testnet (see the code repo). No build step required to view the explainer.

---

## MeshCredit v2 — accurate summary

**The product is the certificate, not any single payment.** MeshCredit issues an on-ledger XLS-70 Credential (the passport) that attests an AI agent's trustworthiness across six independently-verifiable dimensions.

### Principal model

The subject is an AI agent; the principal is pluggable: Organization (KYB), Individual (KYC), parent-agent (delegation), or pseudonymous (capped at the lowest tier). Anti-impersonation: a certificate claim is only valid if the named principal counter-signs the agent key.

### Six dimensions — each has a named issuer and real evidence

| # | Dimension | Evidence |
|---|-----------|----------|
| D1 | Principal / KYB | Swiss registry Zefix — demo uses Novartis AG UID CHE-103.867.266 (cached real public-registry fixture; live API requires credentials) |
| D2 | Human accountability | World ID via IDKit v4 (testable via simulator; orb requires a device) |
| D3 | Code & runtime provenance | Recomputable SHA-256 of the agent harness + skill — anyone can recompute; catches code-swap |
| D4 | On-chain behavioral record | Re-derivable from public XRPL; third-party settlements only |
| D5 | Capability & scope | Principal-signed mandate |
| D6 | Compliance / AML | Real OFAC SDN screening (full list, 19,794 entries) — hard gate, not advisory |

### Tier + confidence (the data flywheel)

Certificates carry a **deterministic Bronze→Platinum tier** and a first-class **confidence level**. A new agent starts at "Bronze, low confidence, 0 settlements"; on-chain history raises it to "Gold, high confidence, N settlements". The behavioral record is public XRPL, so the confidence score is auditable by anyone. Effective spend ceiling = min(tier ceiling, principal remaining delegation budget).

### Enforcement — framed precisely

XRPL consensus enforces credential existence and gating via DepositAuth/DepositPreauth and XLS-80 Permissioned Domains: an uncertified agent's EscrowFinish returns `tecNO_PERMISSION` at consensus. Consensus does **not** validate the score — the MeshCredit bureau enforces dimension integrity via independently-checkable evidence. Treasury is a single signer in the demo; multi-sig/HSM is the production path.

### Agentic runtime

The agent runs on a real frontier LLM (DeepSeek): 6 real reasoning calls per demo run that gate real on-chain actions — plan, per-payment assess (×2), denial reactions, and AML hold.

### Demo arc (real XRPL testnet)

1. KYB Novartis → issue passport (6 dims, Bronze, confidence level)
2. Fan-out settlements to 2 suppliers (EscrowFinish)
3. Three denials that actually bite: tier-ceiling, delegation-cap, and AML-DENY on the real OFAC SDN entity "Star Dragon Corporation Limited" (score 1.0)
4. Uncertified-agent contrast — `tecNO_PERMISSION` returned at consensus
5. Code-swap detection
6. Surgical kill-switch — revoke only the compromised agent; the certified agent keeps paying

### Real verified testnet transactions (2026-06-21 run)

| Event | TX hash |
|-------|---------|
| KYB OperatorCredential | [A2F2270B...](https://testnet.xrpl.org/transactions/A2F2270BAEE41ADD6E4968A0192A2519875A078A7513CE6F9CF4667BEF02DCD9) |
| Bank gate DepositPreauth | [595F2FA8...](https://testnet.xrpl.org/transactions/595F2FA864600A20F08ACCEDAC440CD35A34D0FB5048EA78D567B441385D0F9D) |
| Agent passport CredentialCreate | [1521B5E8...](https://testnet.xrpl.org/transactions/1521B5E868EEAEE2017F0AF76058EEA95B13FAEE0615C0115154B58E031798DC) |
| Settlement A EscrowFinish | [C45EE2DE...](https://testnet.xrpl.org/transactions/C45EE2DE5EF2E082BE352C1B35CE6941721D2A850A7CB24C77C00A2256AD6318) |
| Settlement B EscrowFinish | [0A816BF1...](https://testnet.xrpl.org/transactions/0A816BF1FFA0AD2A389BCB2EA2A652108170EEE6F4658BC8D8F2F68753D93B56) |
| Uncertified contrast (tecNO_PERMISSION) | [2AB0265C...](https://testnet.xrpl.org/transactions/2AB0265CE38A212855482055B568EE083624D333EC48C16C2A2092E5F2A1A410) |
| Kill-switch CredentialDelete | [6D53792D...](https://testnet.xrpl.org/transactions/6D53792D16699E74819DFC9D3B96C6B29A39686F323E261E8B136BF02E4DA9A1) |
| Post-kill confirm EscrowFinish | [87CF6B95...](https://testnet.xrpl.org/transactions/87CF6B950191B1262173CF131B01671C2963F34409E98D49FDA6413AAD1ECC36) |

These are real on-chain transactions; the team may refresh them after the final demo run.

### Business model (the flywheel)

More on-chain data → empirically calibrated thresholds, graph-scale fraud detection, negative-event sharing (consortium), and portable reputation. Relying parties pay per verification; operators pay onboarding and renewal fees to issue agent passports. Industry analogs: credit bureaus (FICO/Experian), fraud consortiums (Early Warning/Sardine), Chainalysis.

### XRPL features used

XLS-70 Credentials, DepositAuth/DepositPreauth, XLS-80 Permissioned Domains, XLS-85 TokenEscrow, DEX path payments, did:xrpl, RLUSD, lightweight x402 compliance gate. Most primitives are Mainnet-ready.

---

## SwissHacks 2026 context

MeshCredit v2 is a submission to the **Ripple Pillar 3 — Agent Financial Infrastructure / KYA** track at SwissHacks 2026. It directly addresses all four Pillar-3 example angles: KYA identity (DID/Credentials/Permissioned Domains), agent wallets with spending policies, regulated settlement including x402, and agent-to-agent delegation. The 40% Viability weight is the primary target.

---

## Honesty notes (always visible)

- Zefix: cached real public-registry data — the live API requires credentials we do not ship.
- World ID: simulator/staging — an orb requires a physical device.
- Treasury: single signer in the demo — multi-sig/HSM is the production path.
- The thick-file agent uses real seeded on-chain history.
- Demo video: placeholder — the team will provide the final recording.
