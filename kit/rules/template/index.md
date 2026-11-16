---
title: "{{FOLDER_NAME}}"
description: "Catalog of intentional files in this folder (file to unique role)."
version: "1.0.0"
status: current
doc_type: template
related:
  - path: ../directory-index.md
  - path: ../path-pattern.md
  - path: ../../MARKDOWN-STANDARD.md
last_updated: "{{LAST_UPDATED}}"
---

# {{FOLDER_NAME}}

Catalog of intentional files in this folder (file to unique role).

**Copy:** this file becomes `README.md` in a new navigable directory. Retarget the links. Set `doc_type` to `index` and omit `related`. Replace every `{{PLACEHOLDER}}`. The rule is [directory-index.md](../directory-index.md).

## Files

| File | Function |
|------|----------|
| {{FILE_NAME}} | {{FILE_FUNCTION}} |

Add or remove rows so the table matches this directory. The cell shape is the [directory index](../../MARKDOWN-STANDARD.md#directory-index). Omit regenerable output, vendor, `.git/`, secrets, and host trees this repository did not create.

When adding, moving, or splitting a path here, follow [path-pattern.md](../path-pattern.md). This skeleton is a directory index, not a [landing page](../../MARKDOWN-STANDARD.md#landing-readme).
