# Contributing Guide

Thanks for your interest in contributing! 🚀  
To ensure consistency and stability, all contributions must be verified against a **Salesforce scratch org** before opening a pull request.

---

## 1) Prerequisites
- [Salesforce CLI (sf)](https://developer.salesforce.com/tools/salesforcecli) installed  
- Access to the Dev Hub (ask a maintainer if you need access)  
- A properly set up local repo (`force-app` or equivalent source directory)

---

## 2) Create a Scratch Org

Every contribution must be tested in a fresh scratch org with the required features enabled.

**Recommended (uses the project scratch definition):**
```bash
sf org create scratch \
  --target-dev-hub <your-dev-hub-username-or-alias> \
  --definition-file config/project-scratch-def.json \
  --set-alias <your-alias>
```

Alternative (simple developer edition):
```bash
sf org create scratch \
  --target-dev-hub <your-dev-hub-username-or-alias> \
  --edition developer \
  --set-alias <your-alias>
```

Open the org to verify it was created:
```bash
sf org open --target-org <your-alias>
```

Set it as your default org for this project:
```bash
sf config set target-org=<your-alias>
```

---

## 3) Deploy Metadata

All contributions must deploy cleanly with no errors. From the project root:
```bash
sf project deploy start --source-dir force-app
```

If you prefer a manifest-based deploy, generate and use manifest/package.xml:
```bash
sf project generate manifest --source-dir force-app --output-dir manifest
sf project deploy start --manifest manifest/package.xml
```

---

## 4) Run Required Tests
Your deployment must pass all relevant Apex test classes with no failures.
At minimum, you should run the core test classes for this repo (ask a maintainer if unsure).

Run them as part of your deployment:
```bash
sf project deploy start --source-dir force-app --tests "CoreTestClass1,CoreTestClass2"
```

Or run them separately (if code is already deployed):
```bash
sf apex run test --tests "CoreTestClass1,CoreTestClass2" --wait 10 --verbose
```

## 5) Run Required Tests
Once your scratch org is validated:
1.  Push your changes to a feature branch.
2.  Confirm all tests pass.
3.  Open a PR and clearly describe the change.
Maintainers may request your scratch org alias for verification.

---

✅ Checklist Before PR
 - [ ] Scratch org created successfully
 - [ ] Metadata deployed without errors
 - [ ] All required Apex tests passed successfully
















