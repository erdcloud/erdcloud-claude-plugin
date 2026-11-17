---
name: erd-from-sql
description: Build or update an ERDCloud diagram from SQL DDL, an existing schema file, or a plain-language description of the data model.
argument-hint: <diagram URL or id> [path to .sql file or description]
allowed-tools: [Read, Glob, Grep]
---

# Create an ERD from SQL

Arguments: $ARGUMENTS

1. The first argument is the ERDCloud diagram URL or id. If it is missing, ask the user for it (an empty diagram can be created in ERDCloud first).
2. Get the schema:
   - If a file path was given, or `.sql` / migration files exist in the project, read them.
   - If only a description was given, write the `CREATE TABLE` statements yourself, with primary keys and `FOREIGN KEY` constraints, and show them to the user for confirmation.
3. Inspect the diagram first (`get_diagram`, `list_tables`, `list_domains`) and tell the user what already exists, so nothing is duplicated.
4. Follow the `erd-modeling` skill: create domains first, then call `import_sql` once with the full DDL so tables and relationships are created together.
5. Verify the result with `list_tables`, report what was created, and mention that a Snapshot can be taken in ERDCloud to keep this version.
