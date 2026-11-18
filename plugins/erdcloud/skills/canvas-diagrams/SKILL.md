---
name: canvas-diagrams
description: This skill should be used when the user asks to draw a sequence diagram, flowchart, UML class diagram, architecture/box diagram or any free-form shapes in ERDCloud (an erdcloud.com/d/<id> link), or to edit shapes and connectors already on the canvas. Explains which ERDCloud MCP tool to use for each diagram type and how to edit the result.
version: 1.0.0
---

# ERDCloud canvas diagrams

An ERDCloud diagram is one canvas. Besides ERD tables it can hold shapes and connectors, so the same diagram can contain a sequence diagram, a flowchart, a UML class diagram or an architecture sketch. All edits are applied live to anyone viewing the diagram.

Read first: `get_diagram` (and `get_snapshot` or `list_shapes` / `list_connectors` to see what is already on the canvas). Place new drawings away from existing objects (use `origin`) and do not delete things the user did not ask about.

## Pick the tool by diagram type

Prefer a one-call generator. They lay everything out automatically; many single-shape calls are slow, easy to get wrong and can hit the rate limit (about 50 calls per 10 seconds per tool).

| Goal | Tool |
|---|---|
| Sequence diagram | `create_sequence_diagram` |
| Flowchart (optionally with swimlanes) | `create_flowchart` |
| UML class diagram | `create_class_diagram` |
| Architecture / free-form drawing, or small edits | `create_shape` + `create_connector`, then `update_shape` / `update_connector` |
| Message numbering of an existing sequence diagram | `set_sequence_options` |

### Sequence diagram

`create_sequence_diagram`: `participants` (names, or `{name, kind: participant|rparticipant|actor|database|boundary|control|entity, bottomHeader?, destroyed?}`) and `messages` `{from, to, text?, reply?, async?, failure?, delay?}` in top-to-bottom order (`reply` = dashed return arrow, `async` = open arrowhead, `failure` = X end, `from == to` = self call). Optional: `notes`, `dividers`, `fragments` (`alt`, `opt`, `loop`, `par`, ... with `fromMessage`/`toMessage` indexes and `elseAt`), `activations`, `autoNumber`, `autoActivation`. Message indexes are 0-based.

### Flowchart

`create_flowchart`: `nodes` `{id, type?, text?}` and `edges` `{from, to, text?, dashed?}`.

- Node types: `start`, `end` (rounded), `process` (default box), `decision` (diamond), `io` (parallelogram), `document`, `subprocess`, `database`, `preparation`, `manual`, `connector` (small circle).
- Put branch labels in the edge `text` (for example `Yes` / `No` on the two edges leaving a decision).
- Loops back to an earlier node are fine.
- `direction`: `TB` (default) or `LR`.
- Swimlanes: `lanes: [{name, nodes: [ids]}]` (top-to-bottom only). Every node must be in exactly one lane.

### UML class diagram

`create_class_diagram`: `classes` `{name, kind?: class|interface, stereotype?, attributes?, methods?}` and `relations` `{from, to, type, label?}`.

- Write members as the text you want shown, with visibility, for example `"- id: int"` and `"+ save(): void"`.
- Relation types: `inherit` (from = child, to = parent), `realize` (from = implementing class, to = interface), `assoc`, `aggregate` and `compose` (from = the whole, where the diamond is drawn), `depend`. Put multiplicity or role in `label`.
- Parents are placed above their children.

### Free-form shapes and connectors

`create_shape` takes `shapeType` from the tool schema: basic shapes, `text`, `frame` (container) and `swimlane` (titled container; objects fully inside move with it), flowchart shapes, UML shapes (`umlClass`, `umlInterface`, `umlPackage`, `umlComponent`, `umlActor`, `umlInitial`, `umlFinal`), general shapes (`cloud`, `cube`, `blockArrow`, `callout`, `star`, `pentagon`, `trapezoid`, `bracket`, `brace`, `folder`, `serverRack`) and the sequence elements.

- For a class-like box, `text` lines are split into compartments by a line containing only `--` (name / attributes / methods).
- Styling: `color` (fill), `strokeColor`, `textColor` (omit to follow the fill automatically, pass an empty string on update to go back to automatic), `fontSize`, `rotation` (flowchart and general shapes).
- `create_connector` connects two object ids (shapes, tables or memos): `lineStyle` straight or elbow, `arrowStart` / `arrowEnd` (`none` or `arrow`), `arrowStyle` and `startStyle` (`filled`, `open`, `x`, `triangle`, `diamond`, `diamondFilled`), `dashed`, `lineWidth`, `label`, `color`. For example inheritance = `arrowEnd: "arrow"`, `arrowStyle: "triangle"`; composition = `arrowStart: "arrow"`, `startStyle: "diamondFilled"`, `arrowEnd: "none"`.
- Routing a line around objects: for `lineStyle: "elbow"`, `bend` (px, -1000..1000) moves the middle segment of the bent line from its default halfway position (up/down for lines that leave the bottom, left/right for lines that leave the side). For full control pass `waypoints: [{x, y}, ...]` (max 12, canvas coordinates, source to target); elbow lines get right-angle corners between the points, straight lines connect them directly. `update_connector` with `waypoints: []` returns to the automatic route. When several elbow lines enter the same object, give each a different `endShift` (px along the object's edge; likewise `startShift` for lines leaving one object) so they run side by side instead of overlapping.

## Limits and tips

- The canvas is 4000 x 4000 px. Generators reject results that would not fit; use fewer nodes, shorter text, or split into several diagrams.
- Positions are snapped to a 10 px grid.
- Generator calls create many objects at once. After creating, report what was made (counts and names), and suggest the user create a Snapshot in ERDCloud before big rewrites.
- To change something afterwards, use `update_shape` / `update_connector` with the ids returned by the generator (or from `list_shapes` / `list_connectors`) instead of recreating the whole diagram.
- `delete_shape` also removes the connectors attached to that shape.

## If a call is rejected with 401

The ERDCloud sign-in is missing or expired. Tell the user to run `/mcp`, select `erdcloud` and sign in again.
