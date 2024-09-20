# Review and check your Statuses

## About this file

This file was created by the Obsidian Tasks plugin (version 7.10.0) to help visualise the task statuses in this vault.

If you change the Tasks status settings, you can get an updated report by:

- Going to `Settings` -> `Tasks`.
- Clicking on `Review and check your Statuses`.

You can delete this file any time.

## Status Settings

<!--
Switch to Live Preview or Reading Mode to see the table.
If there are any Markdown formatting characters in status names, such as '*' or '_',
Obsidian may only render the table correctly in Reading Mode.
-->

These are the status values in the Core and Custom statuses sections.

| Status Symbol | Next Status Symbol | Status Name | Status Type | Problems (if any) |
| ----- | ----- | ----- | ----- | ----- |
| `space` | `x` | Todo | `TODO` |  |
| `x` | `space` | Done | `DONE` |  |
| `/` | `x` | In Progress | `IN_PROGRESS` |  |
| `-` | `space` | Cancelled | `CANCELLED` |  |
| `space` | `x` | incomplete | `TODO` | Duplicate symbol '`space`': this status will be ignored. |
| `x` | `space` | complete / done | `DONE` | Duplicate symbol '`x`': this status will be ignored. |
| `-` | `space` | cancelled | `CANCELLED` | Duplicate symbol '`-`': this status will be ignored. |
| `>` | `x` | deferred | `TODO` |  |
| `/` | `x` | in progress, or half-done | `IN_PROGRESS` | Duplicate symbol '`/`': this status will be ignored. |
| `!` | `x` | Important | `TODO` |  |
| `?` | `x` | question | `TODO` |  |
| `R` | `x` | review | `TODO` |  |
| `+` | `x` | Inbox / task that should be processed later | `TODO` |  |
| `b` | `x` | bookmark | `TODO` |  |
| `B` | `x` | brainstorm | `TODO` |  |
| `D` | `x` | deferred or scheduled | `TODO` |  |
| `I` | `x` | Info | `TODO` |  |
| `i` | `x` | idea | `TODO` |  |
| `N` | `x` | note | `TODO` |  |
| `Q` | `x` | quote | `TODO` |  |
| `W` | `x` | win / success / reward | `TODO` |  |
| `P` | `x` | pro | `TODO` |  |
| `C` | `x` | con | `TODO` |  |

## Loaded Settings

<!-- Switch to Live Preview or Reading Mode to see the diagram. -->

These are the settings actually used by Tasks.

```mermaid
flowchart LR

classDef TODO        stroke:#f33,stroke-width:3px;
classDef DONE        stroke:#0c0,stroke-width:3px;
classDef IN_PROGRESS stroke:#fa0,stroke-width:3px;
classDef CANCELLED   stroke:#ddd,stroke-width:3px;
classDef NON_TASK    stroke:#99e,stroke-width:3px;

1["'Todo'<br>[ ] -> [x]<br>(TODO)"]:::TODO
2["'Done'<br>[x] -> [ ]<br>(DONE)"]:::DONE
3["'In Progress'<br>[/] -> [x]<br>(IN_PROGRESS)"]:::IN_PROGRESS
4["'Cancelled'<br>[-] -> [ ]<br>(CANCELLED)"]:::CANCELLED
5["'deferred'<br>[&gt;] -> [x]<br>(TODO)"]:::TODO
6["'Important'<br>[!] -> [x]<br>(TODO)"]:::TODO
7["'question'<br>[?] -> [x]<br>(TODO)"]:::TODO
8["'review'<br>[R] -> [x]<br>(TODO)"]:::TODO
9["'Inbox / task that should be processed later'<br>[+] -> [x]<br>(TODO)"]:::TODO
10["'bookmark'<br>[b] -> [x]<br>(TODO)"]:::TODO
11["'brainstorm'<br>[B] -> [x]<br>(TODO)"]:::TODO
12["'deferred or scheduled'<br>[D] -> [x]<br>(TODO)"]:::TODO
13["'Info'<br>[I] -> [x]<br>(TODO)"]:::TODO
14["'idea'<br>[i] -> [x]<br>(TODO)"]:::TODO
15["'note'<br>[N] -> [x]<br>(TODO)"]:::TODO
16["'quote'<br>[Q] -> [x]<br>(TODO)"]:::TODO
17["'win / success / reward'<br>[W] -> [x]<br>(TODO)"]:::TODO
18["'pro'<br>[P] -> [x]<br>(TODO)"]:::TODO
19["'con'<br>[C] -> [x]<br>(TODO)"]:::TODO
1 --> 2
2 --> 1
3 --> 2
4 --> 1
5 --> 2
6 --> 2
7 --> 2
8 --> 2
9 --> 2
10 --> 2
11 --> 2
12 --> 2
13 --> 2
14 --> 2
15 --> 2
16 --> 2
17 --> 2
18 --> 2
19 --> 2

linkStyle default stroke:gray
```
