# 12. Cryptography, Transport, and Data Protection Controls

Category ID: 12

Category name: Cryptography, Transport, and Data Protection Controls

## Purpose

Review whether encryption, hashing, signing, transport security, certificate validation, random generation, password protection, key lifecycle, and data-protection controls are appropriate for the data, system, environment, and threat model.

## Core Review Question

Are encryption, hashing, signing, transport security, certificate validation, random generation, password protection, and data-protection controls appropriate for the data, system, environment, and threat model?

## Scope

TLS/HTTPS/HSTS/mixed content/certificates/mTLS, encryption at rest/field/envelope/database/storage/backup/log/file/export, password hashing/KDFs/salts, randomness/nonces/IVs/tokens/reset links/session IDs, JWT/message/webhook signing, KMS/key vault/HSM/key lifecycle/separation/rotation/revocation/access, masking/tokenization/pseudonymization/anonymization/deletion, and vendor/SaaS/AI encryption claims.

## Review Signals

- Sensitive data, credentials, or private records move over transport paths whose protection is unclear.
- Certificate validation, trust model, TLS behavior, signing verification, or fail-closed behavior is unclear.
- Passwords, reset links, session IDs, random values, private keys, signing keys, encryption keys, or production crypto material appear in unsafe locations.
- Vendor/SaaS/AI encryption claim is used as approval without data-use, retention, key access, or decrypt path details.
- Current vulnerability, algorithm, library, platform, or vendor guidance may affect the decision.

## Red Conditions

- Sensitive data/credentials sent over unprotected transport.
- Certificate validation disabled or trust-any behavior in production/sensitive use.
- Plaintext, reversible, unsalted, or fast-hashed passwords for real users.
- Private/signing/encryption keys or production crypto material exposed or shared unsafely.
- Missing or fail-open signing/integrity verification for sensitive trust-boundary messages.
- Production crypto keys reused in test, demo, local, AI, vendor, or uncontrolled workflows.
- Unreviewed custom or AI-generated cryptography protects real sensitive assets.
- Sensitive backups, exports, logs, or files unencrypted or weakly protected in unsafe sharing/storage.
- Predictable security tokens, reset links, session IDs, nonces, IVs, or salts affect real security decisions.

## Orange Conditions

- Transport protection incomplete or uncertain.
- Invalid, self-signed, or unmanaged certificate in sensitive context.
- Weak/deprecated TLS, cipher, algorithm, library, or parameter suspected.
- Password hashing parameters unknown or weak.
- Token/JWT/webhook/message validation incomplete.
- Encryption at rest exists but decrypt access, key ownership, or field-level need unknown.
- Vendor/SaaS/AI encryption claim insufficient.
- Key lifecycle, rotation, revocation, access, or separation unclear.
- Client-side/E2E trust model unclear.
- Custom/AI crypto deployment or review unknown.
- Masking, tokenization, anonymization, or deletion claims need owner review.
- Current vulnerability/platform/vendor behavior may affect risk.

## Yellow Conditions

- Certificate renewal, monitoring, ownership, or inventory gap.
- Low-risk HTTPS/HSTS/redirect/mixed-content hygiene issue.
- Approved encryption/KMS/key vault/HSM/managed TLS lacks documentation.
- Password hashing tuning or migration contained.
- Publishable key restriction documentation gap.
- Crypto library/TLS/cert automation/platform update needs ticketing.
- Secure-transfer process needs ownership.
- Source freshness re-check needed before live advice.

## Green Conditions

- HTTPS/TLS enforced and transport path documented.
- Self-signed/private-CA cert limited to controlled internal/local/test trust context.
- Managed TLS, encryption, KMS, key vault, HSM, service mesh, or cloud control matches data risk.
- Approved password hashing with appropriate salts/parameters.
- Token/JWT/message/webhook verification uses approved libraries and fails closed.
- Visible key/client ID documented publishable and restricted.
- Synthetic/local examples only.
- Standard crypto libraries and approved key management used.
- External sharing uses approved secure transfer and data-governance controls.

## Gray Conditions

- HTTPS redirect/mixed content/backend transport, cert validation/trust model, hash purpose/security role, signing validation, decrypt access, vendor encryption access/retention/key-management/approval context, client-side/E2E trust model, key lifecycle/secure deletion, or randomness/nonce/IV/reset-link/token/salt source unknown.

## Required Evidence

- Data sensitivity.
- Transport path.
- Certificate validation.
- Algorithm/library/version/current guidance.
- Password hashing parameters.
- Key ownership, storage, rotation, and access.
- Verification failure behavior.
- Secure deletion scope.
- Vendor/platform current docs.

## Owners

Security owner, developer, cloud/platform owner, infrastructure/network owner, data owner, privacy owner, vendor owner, and AI governance owner.

## Non-Dev Action Checks

Do not ignore certificate warnings for sensitive work, share private keys or hashes, rely on "encrypted" as approval, or send sensitive data over unclear channels. Ask security/platform owners for approved secure-transfer and key-management paths.

## Unsafe Request Boundaries

Do not request private keys, password hashes tied to users, raw tokens, downgrade tests, exploit proof, or live credential validation. Use redacted configuration summaries and owner-confirmed controls.

## Safe Evidence Handling

Use redacted TLS/certificate summaries, key-management summaries, library/version names, secure-transfer process summaries, and current official docs. Do not include secrets, keys, hashes tied to users, or private data.

## False-Positive Guardrails

Do not mark Green because data is "encrypted", a vendor says "secure", HTTPS exists somewhere, or a library is popular. Confirm transport path, key access, validation, failure behavior, and data-governance controls.

## Under-Classification Guardrails

Treat disabled cert validation, unclear password hashing, custom crypto, unknown key lifecycle, vendor encryption claims, and current vulnerability status as Orange or Red until reviewed.

## Currentness Notes

Check current TLS, algorithm, library, certificate, platform, vendor, CVE/advisory, and password-hashing guidance where material.

## Category Gate Rule

Fails on unprotected sensitive transport, disabled cert validation in sensitive use, unsafe password/crypto/key handling, missing verification at trust boundaries, or unresolved crypto context for sensitive assets.
