# 08. File, Object, Content, and Storage Handling

Category ID: 08

Category name: File, Object, Content, and Storage Handling

## Purpose

Review whether files, objects, storage locations, generated content, uploads, downloads, previews, and shared content are protected with correct access control, safe processing, safe storage, safe metadata handling, and safe exposure boundaries.

## Core Review Question

Are files, objects, storage locations, generated content, uploads, downloads, previews, and shared content protected with correct access control, safe processing, safe storage, safe metadata handling, and safe exposure boundaries?

## Scope

Files, uploads, downloads, attachments, generated reports, documents, media, archives, backups, dumps, logs, source archives, object/blob storage, buckets/folders/ACL/IAM, signed/pre-signed/SAS URLs, shared links, previews, rendering, indexing, OCR, conversion, metadata, caches, CDN mirrors, and vendor/AI/no-code/support file workflows.

## Review Signals

- File, bucket, folder, object, link, artifact, generated report, backup, dump, export, or source archive may contain sensitive content.
- Signed link, shared link, cache, CDN, preview, conversion, archive extraction, or metadata path may bypass intended access.
- Upload processing handles untrusted files with production or sensitive reach.
- Vendor, AI, no-code, support, or external file workflow receives sensitive files.

## Red Conditions

- Sensitive private files/objects publicly accessible.
- Public listing exposes sensitive files, names, or storage structure.
- Backups, dumps, logs, source archives, or old exports public or broadly shared.
- Generated files include wrong-scope or excessive sensitive data.
- File operation crosses ownership or permission boundaries.
- Secrets/credentials exposed through files, artifacts, storage, links, or logs.
- Signed/shared/access-granting links expose sensitive content beyond intended audience.
- Unsafe upload/file processing path handles untrusted content with sensitive impact.
- Private file cache/CDN/preview mirror remains accessible after revocation.
- Sensitive files sent to unapproved vendor/AI/no-code/support workflow.

## Orange Conditions

- Public/broad file or storage access with unknown contents/approval.
- Signed link scope, expiry, revocation, or logging unknown.
- Upload/download/preview/archive/conversion controls unknown.
- Generated file scoping unknown.
- Backup/artifact/log contents and retention unclear.
- Vendor/AI/support file handling unknown.

## Yellow Conditions

- Non-sensitive file listing/storage metadata hygiene issue.
- Controlled signed link lacks documentation or expiry review.
- Low-risk upload/scanning documentation gap.
- Private cache/retention rationale needs documentation.
- File metadata minimization improvement.

## Green Conditions

- Intentionally public non-sensitive approved static/marketing content.
- Private files access-controlled, least-privilege, audited, and retained appropriately.
- Signed links scoped, short-lived, revocable, auditable, and intended-recipient only.
- Uploads authenticated/authorized, limited, isolated, scanned where needed, and safely served.
- Untrusted processing isolated/resource-limited.
- Generated exports correctly scoped and retained.

## Gray Conditions

- File sensitivity, access audience, link controls, upload/processing isolation, cache behavior, generated-file scope, vendor/tool handling, or artifact contents unknown.

## Required Evidence

- File/data category.
- Access audience.
- Object/storage policy.
- Link expiry and revocation.
- Processing path.
- Cache/CDN behavior.
- Generated-file scoping.
- Retention.
- Vendor/tool handling.
- Current provider behavior where material.

## Owners

Cloud/platform owner, developer, data owner, privacy owner, security owner, vendor owner, operations owner, and AI governance owner.

## Non-Dev Action Checks

Do not make buckets/folders public, post signed links broadly, upload sensitive files to unapproved tools, or share file-list screenshots with sensitive names. Use approved storage, named access, redacted summaries, and synthetic files.

## Unsafe Request Boundaries

Do not request live signed URLs, private file names, object paths, raw files, screenshots with sensitive names, or proof by opening private content. Use redacted path/type summaries and owner-confirmed access settings.

## Safe Evidence Handling

Use redacted summaries, synthetic files, storage policy summaries, link control summaries, processing architecture, retention summaries, and current provider docs when behavior matters.

## False-Positive Guardrails

Do not mark Green because a link is hard to guess, a bucket is obscure, a file is "old", a preview is cached, or content is "internal". Confirm access policy, audience, contents, expiry, and revocation.

## Under-Classification Guardrails

Treat backups, dumps, source archives, generated reports, logs, signed links, shared folders, and vendor/AI file handling as sensitive until contents and access are confirmed.

## Currentness Notes

Check current storage provider, signed-link, CDN/cache, preview, upload scanning, conversion, and vendor/AI file-handling behavior when those facts affect risk.

## Category Gate Rule

Fails on public/broad sensitive file exposure, wrong-scope generated files, unsafe file operations, exposed credential-bearing artifacts, or unresolved sensitive storage/link/file-processing unknowns.
