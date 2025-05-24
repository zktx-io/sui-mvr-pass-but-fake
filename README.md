# 🧾 Report: MVR Pass Without Source

## 1. Purpose of This Repository

This repository (`sui-mvr-pass-but-fake`) is a **demonstration of a validation limitation** in the current **Move Registry (MVR)** flow.

It is intentionally configured to contain **no source code**, yet it still **successfully passes** MVR’s version creation process by submitting a valid-looking `Move.lock` file.

This is **not intended as an attack**, but rather as a **practical test case** to explore how the current system behaves under minimal input.

The goal is to highlight that:

- **MVR validation focuses on configuration, not source integrity**
- **Honest submission is currently assumed**, but not enforced
- There’s an opportunity to **enhance trust** through stronger, cryptographic provenance

## 2. Context: What MVR Currently Checks

During version creation, MVR performs several reasonable checks:

- Ensures the GitHub repository is **public**
- Downloads the `Move.lock` file at the specified commit
- Validates that fields like `published-version` and `original-published-id` match

However, it **does not** check:

- Whether the commit actually **built the deployed package**
- Whether any **source code exists** in the repository
- Whether the `Move.lock` reflects a **real or reproducible build**

The version submission UI already includes the following helpful disclaimer:

> **"This does not verify the source, it only verifies the configuration, and can end up with many false positives."**

📸 **Validation Warning Modal**  
<img src="./screenshots/modal-warning.png" alt="Validation Warning Modal" width="480"/>

This warning is clear — and appreciated.  
Yet, as this repository shows, even a completely empty project can still **pass validation with no friction**, as long as it includes a syntactically valid `Move.lock` file.

## 3. Validation Passes with No Code

This repository contains only:

- A `Move.lock` file with **hardcoded dependency metadata**
- **No** `sources/` directory
- **No** modules or transaction scripts

Despite this, the registry **accepts the submission as valid**:

📸 **Validation Passed Screenshot**  
<img src="./screenshots/validation-passed.png" alt="Validation Passed" width="480"/>

This doesn’t mean the registry is broken —  
but it does demonstrate that **proof of configuration** is not the same as **proof of build or source authenticity**.

## 🧩 Conclusion

This example highlights a **gap between configuration-based validation and cryptographically verifiable provenance**.

The current MVR design provides a good starting point, especially with visible disclaimers and guardrails.  
But to **scale trust in a decentralized ecosystem**, we believe it’s important to evolve toward:

- **Automated GitHub CI workflows** that generate `.intoto.jsonl` provenance files  
- **Signature verification** that proves the connection between source, build, and on-chain deployment

We present this repository not as a criticism, but as a **constructive prompt** for the ecosystem to explore what's possible next.

## 🔗 Related Repositories

- [sui-mvr-provenance](https://github.com/zktx-io/sui-mvr-provenance): Full provenance design and examples  
- [sui-mvr-example](https://github.com/zktx-io/sui-mvr-example): A verifiable reference implementation with reproducible builds

## 🔍 Learn More

- [docs.zktx.io/slsa/mvr](https://docs.zktx.io/slsa/mvr): Detailed documentation on how provenance workflows integrate with MVR and SLSA