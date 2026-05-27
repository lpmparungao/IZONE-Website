# Git Branching Workflow

## Branch Structure

### Main Branches

#### `main`
- Production code
- Always stable
- Tagged for every release

#### `development`
- Integration branch for all completed work
- Where features come together

#### `release/vX.Y.Z`
- Temporary QA + stabilization branch
- Created only when preparing a release

Example:
```bash
release/v1.1.0
```

---

# Workflow

## 1. Start Work

Create a feature branch from `development`:

```bash
feature-<name>
```

Example:
```bash
feature-login
```

---

## 2. Finish Work → Merge to Development

Once done:

- Open a Pull Request
- Merge into `development`
- Must be tested before merge

Flow:
```bash
feature-<name> → development
```

---

## 3. Prepare for QA

When ready for testing:

Create a release branch:

```bash
development → release/v1.1.0
```

---

## 4. QA Testing

QA tests ONLY the release branch:

```bash
release/v1.1.0
```

If bugs are found:

- Fix bugs directly on `release/v1.1.0`

---

## 5. Release to Production

When QA is approved:

```bash
release/v1.1.0 → main
```

Then create a tag:

```bash
v1.1.0
```

---

## 6. Sync Back to Development (IMPORTANT)

After release is completed:

You MUST merge release changes back into `development`
to avoid losing fixes.

Flow:
```bash
release/v1.1.0 → development
```

---

## 7. Bugs From Production

If bugs are found after release:

Create a bugfix branch from `main`:

```bash
bugfix-<name>
```

### Option A — Deploy Bugfix Immediately

```bash
bugfix-<name> → release/v1.1.1
```

Then:
- QA
- Merge into `main`
- Merge into `development`

---

### Option B — Include Bugfix in Next Update

```bash
bugfix-<name> → development → release/v1.2.0
```

Then:
- QA
- Merge into `main`
- Merge into `development`

---

# Example Flow

```text
main
 └── development
      ├── feature-login
      ├── feature-dashboard
      └── release/v1.1.0
```

---

# Recommended Rules

- Never commit directly to `main`
- Never commit directly to `development`
- All work must go through Pull Requests
- QA only tests release branches
- Always sync release branches back to `development`
- Tag every production release
- Keep branch names consistent
