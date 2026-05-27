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
<img width="1919" height="1034" alt="image" src="https://github.com/user-attachments/assets/4f1c252e-0354-4386-9be2-289177842e43" />
<img width="1919" height="1033" alt="image" src="https://github.com/user-attachments/assets/d9c64f36-7043-4f20-8a68-388122553c16" />
<img width="1912" height="1037" alt="image" src="https://github.com/user-attachments/assets/c78eda47-3fd9-44ec-8fb4-5fb09537f0a4" />
<img width="1919" height="1034" alt="image" src="https://github.com/user-attachments/assets/b16d5f57-07d5-4f82-bee4-fea498a494e6" />
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
<img width="1887" height="935" alt="image" src="https://github.com/user-attachments/assets/0558af14-b999-436e-b694-ebfe028e42bf" />
<img width="1896" height="938" alt="image" src="https://github.com/user-attachments/assets/e7eeb3d0-0cf3-498b-be8e-2cdd12bc3f50" />
<img width="1886" height="916" alt="image" src="https://github.com/user-attachments/assets/083b94e6-4431-496b-b1e1-2f359aeace2b" />
<img width="1889" height="937" alt="image" src="https://github.com/user-attachments/assets/800c9890-c031-4199-9b80-d29f13635d0b" />
---

## 3. Prepare for QA

When ready for testing:

Create a release branch:

```bash
development → release/v1.1.0
```
<img width="1888" height="934" alt="image" src="https://github.com/user-attachments/assets/498f0905-a87f-4a6e-bfb4-a5ee26a54055" />
<img width="1884" height="898" alt="image" src="https://github.com/user-attachments/assets/4d960eaf-5c48-472f-b304-3a1b5e0f10ed" />
<img width="1895" height="936" alt="image" src="https://github.com/user-attachments/assets/06293865-e8be-484c-a308-e9568ceac8cf" />
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
<img width="1893" height="942" alt="image" src="https://github.com/user-attachments/assets/a5e4d0e0-ff79-4f54-ae74-c33cfe48a243" />
<img width="1895" height="937" alt="image" src="https://github.com/user-attachments/assets/5180eaaa-c74b-4771-89f9-562f6c67a642" />
<img width="1880" height="929" alt="image" src="https://github.com/user-attachments/assets/a49829e8-ad54-43a0-a0ff-e3f858394c6a" />
<img width="1895" height="933" alt="image" src="https://github.com/user-attachments/assets/b3d25303-dae5-4610-b295-07c269367166" />
<img width="1884" height="933" alt="image" src="https://github.com/user-attachments/assets/f347f04b-fdbc-4792-860f-2b06fef13226" />

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
