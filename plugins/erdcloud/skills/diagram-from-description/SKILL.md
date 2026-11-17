---
name: diagram-from-description
description: Draw a sequence diagram, flowchart or UML class diagram in an ERDCloud diagram from a plain-language description, a process, or existing source code.
argument-hint: <diagram URL or id> <sequence | flowchart | class> <description or path>
allowed-tools: [Read, Glob, Grep]
---

# Draw a diagram in ERDCloud

Arguments: $ARGUMENTS

1. The first argument is the ERDCloud diagram URL or id. If it is missing, ask for it (an empty diagram can be created in ERDCloud first).
2. The second argument is the kind: `sequence`, `flowchart` or `class`. If it is missing, infer it from the description (an interaction between systems over time = sequence, a process or decision logic = flowchart, types and their relationships = class) and say which you chose.
3. Get the content:
   - If a file or directory path was given, read the relevant code (for `class`, the type declarations and their inheritance/implementation/composition relationships; for `sequence`, the call flow of the described use case).
   - Otherwise work from the description. State your assumptions briefly.
4. Inspect the diagram first (`get_diagram`, `list_shapes`) so the new drawing does not overlap what is already there; pass an `origin` below or beside existing objects.
5. Follow the `canvas-diagrams` skill: call exactly one generator (`create_sequence_diagram`, `create_flowchart` or `create_class_diagram`). Keep it readable: at most about 12 participants / 25 nodes / 15 classes per diagram; split bigger systems into several diagrams.
6. Report what was created (names and counts) and mention that a Snapshot can be taken in ERDCloud to keep this version.
