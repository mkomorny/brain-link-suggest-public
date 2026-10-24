---
name: brain-link-suggest
description: >-
  Surfaces unlinked memories across projects that share concepts, libraries, protocols,
  or architectural solutions, and proposes explicit knowledge graph links to build a richer Second Brain.
---

# Brain Link Suggest — Graph Connection Finder (`/brain-link-suggest`)

Use this skill to turn isolated memories into an interconnected knowledge graph by discovering hidden connections and synergies across projects.

---

## What Happens When Invoked

When `/brain-link-suggest` is triggered, execute these steps:

### Step 1: Identify Topic & Search Candidates
1. Take the current project or specified topic name.
2. Query `second-brain` using `recall` with `--hops 1` to find the core cluster of memories for this project.
3. Query `second-brain` with semantic search across the broader database to find memories in *other* projects that share:
   - Identical technology stacks (e.g. WebSocket, WebView2, OSC, WebAudio, SQLite, Basic Pitch)
   - Common architectural patterns (e.g. state machines, event emitters, retry loops)
   - Cross-project dependencies or hardware requirements (e.g. Ableton Live 12, Windows paths, GPU requirements)

### Step 2: Check Existing Connections
Call `connections(id: "<source_id>")` for the project's primary entries to see what links already exist and avoid proposing duplicate graph edges.

### Step 3: Propose Meaningful Graph Edges
For each discovered synergy, determine the relationship type:
- `drawn_from`: Technique in project B was inspired by or derived from project A
- `relates_to`: General conceptual or technical relationship
- `part_of_project`: Component of a broader system
- `supersedes`: Modern pattern replaces an older approach

### Step 4: Output Proposal Table
Display the proposed links in a clear table:
| Source Memory | Target Memory | Proposed Link Type | Synergy / Reason |
| :--- | :--- | :--- | :--- |
| `mem_8f93a1` (OSC Handshake) | `mem_2b1c4e` (MIDI Bridge) | `drawn_from` | Shares heartbeat retry algorithm |

Provide ready-to-run commands:
```
/brain link mem_8f93a1 mem_2b1c4e drawn_from
```
If the user confirms, call the `link` tool immediately.

---

## Syntax

```
/brain-link-suggest [optional memory_id or topic]
```

## Examples

```
/brain-link-suggest
/brain-link-suggest Live Actions
/brain-link-suggest mem_8f93a1
```
