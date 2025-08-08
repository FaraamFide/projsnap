# Projsnap: Project Snapshot Utility

`projsnap` is a CLI utility that creates a single-file text snapshot of a project. The snapshot includes the complete directory tree and the contents of whitelisted source files, making it ideal for archiving, code reviews, or providing context to AI models.

## Installation

To install `projsnap` and make it available as a system-wide command:

1.  **Make the script executable:**
    ```bash
    chmod +x projsnap
    ```

2.  **Move it to a directory in your system's PATH.** `/usr/local/bin` is recommended.
    ```bash
    sudo mv projsnap /usr/local/bin/
    ```

3.  **Verify the installation:**
    ```bash
    projsnap --help
    ```

## Setup

The utility requires a `_snapshots/_snapshot.txt` file in the project root.

```
project_root/
├── _snapshots/
│   └── _snapshot.txt
└── ... (other project files)
```

## Configuration (`_snapshot.txt`)

This file defines exclusion rules for the file *content* section.

-   Lines starting with `#` are ignored comments.
-   Each line specifies a pattern to exclude:
    -   **Directories:** `node_modules`, `dist`
    -   **File Extensions:** `.log`, `.tmp`
    -   **Specific Files:** `README.md`

## Key Feature: Tree vs. Content

The snapshot separates structure from content:

-   The `PROJECT STRUCTURE` section shows the **full project tree**.
-   Excluded directories (e.g., `node_modules`) are listed but **not expanded**.
-   The `FILE CONTENTS` section only includes files that are whitelisted and not explicitly excluded by the rules.

## Usage

Run `projsnap` from the project's root directory.

**Flags:**
-   `-n, --name <filename>`: Sets a custom name for the snapshot file.
-   `-y, --yes`: Skips all interactive prompts for non-interactive use.

**Examples:**
```bash
# Create a snapshot with a custom name
projsnap --name my-feature

# Create it non-interactively
projsnap -n my-feature -y
```

## Output Format

The generated file has a clear, structured format.

```
# Snapshot generated on: ...
# Exclusion patterns used: [...]

--- PROJECT STRUCTURE ---
.
├── node_modules
├── src
│   └── main.ts
└── package.json

--- FILE CONTENTS ---


# ─── FILE: src/main.ts ────────────────────────────────────────────────────
console.log("Hello, World!");


# ─── FILE: package.json ───────────────────────────────────────────────────
{
  "name": "my-project",
  "version": "1.0.0"
}
```
