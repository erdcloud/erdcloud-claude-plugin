---
name: erd-modeling
description: This skill should be used when the user asks to create, edit, review or extend an ERD (entity relationship diagram) in ERDCloud, mentions an erdcloud.com/d/<id> link, or asks to add tables, columns, relations, domains or memos to a diagram. Explains the correct order of operations for the ERDCloud MCP tools.
version: 1.0.0
---

# ERDCloud modeling

Use the `erdcloud` MCP server tools (`mcp__erdcloud__*`) to read and edit ERD diagrams. All edits are applied live to anyone viewing the diagram.

A diagram is identified by its id or its URL, for example `https://www.erdcloud.com/d/<id>`. Ask the user for it if it was not given.

## Before editing

1. Read first: `get_diagram`, `list_tables`, `list_domains` (and `get_table` for details) so you reuse what already exists instead of duplicating it.
2. For large changes, advise the user to create a Snapshot or export a backup in ERDCloud first. AI edits can be wrong and a snapshot is the easy way back.
3. Summarize the planned change and confirm before deleting tables, columns or relations.

## Domain-first workflow

Do not leave a column's type as a bare string with an empty domain.

1. Register one reusable domain per distinct data type with `create_domain`, using a short name and the real DB type as the domain's `type`. Examples: `varchar(8)` -> `var8`, `varchar(255)` -> `var255`, `int` -> `int`, `bigint` -> `bigint`, `decimal(10,2)` -> `dec10_2`, `datetime` -> `datetime`, `boolean` -> `bool`.
2. When creating columns (`create_table` `columns` or `add_column`), set each column's `domain` to the matching domain name.
3. Reuse the same domain for every column of that type.

## Relationship workflow

A relationship can only connect tables that already exist, so order matters.

- Preferred for any schema with related tables: call `import_sql` once with the full `CREATE TABLE` (+ `FOREIGN KEY`) DDL. It creates every table and wires all relationships in one call.
- Building tables one by one: create ALL tables first with `create_table`, then connect them with `create_relation` (both the child and the parent table must exist). `create_table` alone never links tables.

## Batch tools

Prefer `update_tables` and `update_columns` over many single-item calls when changing several tables or columns.

## Tool overview

| Area | Tools |
|---|---|
| Read | `get_diagram`, `list_tables`, `get_table`, `list_memos`, `list_domains`, `get_snapshot` (also returns shapes and connectors) |
| Tables | `create_table`, `update_table`, `update_tables`, `delete_table`, `import_sql` |
| Columns | `add_column`, `update_column`, `update_columns`, `delete_column` |
| Relations | `create_relation`, `delete_relation` |
| Domains | `create_domain`, `update_domain`, `delete_domain` |
| Memos | `create_memo`, `update_memo`, `delete_memo` |
| Canvas drawings (shapes, connectors, sequence diagrams, flowcharts, UML class diagrams) | see the `canvas-diagrams` skill: `list_shapes`, `list_connectors`, `create_shape`, `create_connector`, `create_sequence_diagram`, `create_flowchart`, `create_class_diagram`, ... |

## If a call is rejected with 401

The ERDCloud sign-in is missing or expired, or the user disconnected the app in ERDCloud. Tell the user to run `/mcp` in Claude Code, select `erdcloud` and sign in again. Connected apps can be reviewed and disconnected in ERDCloud (open a diagram, then the AI (MCP) panel).
