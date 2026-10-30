# Docker Image Tags Reference

This document describes the Docker image tagging strategy for the Python project.

## Tag Naming Convention

All images use the format: `snowdreamtech/python:TAG`

Where `TAG` follows these patterns:

- **Variant-specific tags**: `TAG-variant` (e.g., `nightly-alpine`, `3.14.7-alpine`)
- **Default tags** (Debian only): `TAG` (e.g., `nightly`, `latest`, `3.13.5`)

## Supported Registries

All tags are pushed to two registries:

- **DockerHub**: `snowdreamtech/python:TAG`
- **GitHub Container Registry**: `ghcr.io/snowdreamtech/python:TAG`

## Tag Scenarios

### 1. Branch Builds (dev/main)

#### Push to `dev` branch

```bash
git push origin dev
```

**Generated tags:**

```
snowdreamtech/python:dev-alpine
snowdreamtech/python:dev-debian
snowdreamtech/python:dev              # ← Debian (default)
snowdreamtech/python:dev-rocky
```

#### Push to `main` branch

```bash
git push origin main
```

**Generated tags:**

```
snowdreamtech/python:main-alpine
snowdreamtech/python:latest-alpine
snowdreamtech/python:main-debian
snowdreamtech/python:latest-debian
snowdreamtech/python:main             # ← Debian (default)
snowdreamtech/python:latest           # ← Debian (default)
snowdreamtech/python:main-rocky
snowdreamtech/python:latest-rocky
```

---

### 2. Release Tags (Semantic Versioning)

#### Alpine Release

```bash
git tag alpine-v3.14.7
git push origin alpine-v3.14.7
```

**Generated tags:**

```
snowdreamtech/python:3.14.7-alpine
snowdreamtech/python:latest-alpine
```

#### Debian Release

```bash
git tag debian-v3.13.5
git push origin debian-v3.13.5
```

**Generated tags:**

```
snowdreamtech/python:3.13.5-debian
snowdreamtech/python:latest-debian
snowdreamtech/python:3.13.5           # ← Debian (default)
snowdreamtech/python:latest           # ← Debian (default)
```

#### Rocky Release

```bash
git tag rocky-v3.12.13
git push origin rocky-v3.12.13
```

**Generated tags:**

```
snowdreamtech/python:3.12.13-rocky
snowdreamtech/python:latest-rocky
```

---

### 3. Nightly Builds (Scheduled)

**Trigger:** Automatically every day at 17:00 UTC

**Generated tags:**

```
# Alpine
snowdreamtech/python:nightly-alpine
snowdreamtech/python:20260427-alpine

# Debian (with default tags)
snowdreamtech/python:nightly-debian
snowdreamtech/python:20260427-debian
snowdreamtech/python:nightly          # ← Debian (default)
snowdreamtech/python:20260427         # ← Debian (default)

# Rocky
snowdreamtech/python:nightly-rocky
snowdreamtech/python:20260427-rocky
```

---

## Tag Priority

Tags are generated with the following priority (higher number = higher priority):

| Priority | Type | Example Tags | Trigger |
|----------|------|--------------|---------|
| 1000 | Nightly | `nightly`, `nightly-alpine` | Schedule |
| 900 | Date | `20260427`, `20260427-alpine` | Schedule |
| 800 | Version | `3.14.7-alpine`, `3.13.5` | Tag push |
| 600 | Branch | `dev-alpine`, `main-debian` | Branch push |
| 200 | Latest | `latest`, `latest-alpine` | Main/Tag |

---

## Default Variant (Debian)

Debian is designated as the **default variant** (`is_latest: true`), which means:

✅ **Debian gets BOTH suffixed AND unsuffixed tags:**

```
snowdreamtech/python:nightly-debian   # Variant-specific
snowdreamtech/python:nightly          # Default (no suffix)

snowdreamtech/python:3.13.5-debian    # Variant-specific
snowdreamtech/python:3.13.5           # Default (no suffix)

snowdreamtech/python:latest-debian    # Variant-specific
snowdreamtech/python:latest           # Default (no suffix)
```

❌ **Alpine and Rocky get ONLY suffixed tags:**

```
snowdreamtech/python:nightly-alpine   # Variant-specific only
snowdreamtech/python:nightly-rocky    # Variant-specific only
```

---

## Usage Examples

### Pull the latest Debian image (default)

```bash
docker pull snowdreamtech/python:latest
# or
docker pull snowdreamtech/python:latest-debian
```

### Pull the latest Alpine image

```bash
docker pull snowdreamtech/python:latest-alpine
```

### Pull the latest Rocky image

```bash
docker pull snowdreamtech/python:latest-rocky
```

### Pull a specific version

```bash
# Alpine 3.14.7
docker pull snowdreamtech/python:3.14.7-alpine

# Debian 3.13.5 (two ways)
docker pull snowdreamtech/python:3.13.5-debian
docker pull snowdreamtech/python:3.13.5

# Rocky 3.12.13
docker pull snowdreamtech/python:3.12.13-rocky
```

### Pull nightly builds

```bash
# Alpine nightly
docker pull snowdreamtech/python:nightly-alpine

# Debian nightly (two ways)
docker pull snowdreamtech/python:nightly-debian
docker pull snowdreamtech/python:nightly

# Rocky nightly
docker pull snowdreamtech/python:nightly-rocky
```

---

## Tag Lifecycle

### Development Flow

```
1. Push to dev → python:dev-alpine, python:dev-debian, python:dev, python:dev-rocky
2. Push to main → python:main-alpine, python:latest-alpine, python:main-debian, python:latest-debian, python:main, python:latest, python:main-rocky, python:latest-rocky
3. Create tag → python:VERSION-variant, python:latest-variant (+ unsuffixed for Debian)
```

### Release Flow (with Release Please)

```
1. Merge PR to main → Release Please creates release PR
2. Merge release PR → Release Please creates tags (alpine-vX.Y.Z, debian-vX.Y.Z, rocky-vX.Y.Z)
3. Tag push triggers build → Images published with version tags
```

---

## Matrix Configuration

The workflow uses a matrix strategy with three variants:

```yaml
matrix:
  include:
    - variant: alpine
      version: "3.14.7"
      is_latest: false

    - variant: debian
      version: "3.13.5"
      is_latest: true    # ← Default variant

    - variant: rocky
      version: "3.12.13"
      is_latest: false
```

Only the variant with `is_latest: true` receives unsuffixed tags.

---

## Metadata Action Configuration

The key configuration that enables this tagging strategy:

```yaml
images: |
  name=ghcr.io/snowdreamtech/python,enable=true
  name=snowdreamtech/python,enable=true
flavor: |
  latest=false
  prefix=
  suffix=-${{ matrix.variant }}  # ← Adds variant suffix to all tags
```

For Debian (is_latest), additional rules generate unsuffixed tags:

```yaml
type=raw,enable=${{ matrix.is_latest }},priority=1000,prefix=,suffix=,pattern=nightly
```

This creates both `nightly-debian` (from flavor suffix) and `nightly` (from this rule).
