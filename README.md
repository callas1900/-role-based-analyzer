# role-based-analyzer

A Claude Code plugin for analyzing the current structure of a business field's workflow inside a company — as a precondition for process improvement.

## What it does

Invokes a structured interview covering three dimensions of your framework:

- **Role** — person-independent roles defined by Name, Purpose, Domain, and Accountabilities (Holacracy-based)
- **Artifacts** — deliverables and submitted items, with optional internal parts (`Artifact::part`)
- **Meetings** — defined by requirement documents, participant criteria, agenda items, output documents, and meeting-specific roles (`Meeting::Role`)

After the interview, the skill writes a single structured markdown report capturing all captured entities.

> **Out of scope:** dynamic relationships across dimensions, temporal concepts, and edge cases.

## Installation

Run these two commands inside a Claude Code session (replace the path with your actual checkout location):

```text
/plugin marketplace add /path/to/role-based-analyzer
/plugin install role-based-analyzer@role-based-analyzer-local
```

For quick local development without registering a marketplace, launch Claude Code with:

```sh
claude --plugin-dir /path/to/role-based-analyzer
```

## Usage

Type `/role-based-analyzer` in a Claude Code session to start the interview.

## Author

callas1900
