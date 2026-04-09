# Style & Organization Rules

## Unused Variables

| | |
|---|---|
| **Rule ID** | UnusedVariables |
| **Severity** | Warning |

Variables declared in the Blueprint (including Event Dispatchers) that are never referenced in any graph.

**Reference detection covers:**

- Direct Get and Set nodes
- Event Dispatcher operations: Call, Bind (Assign/AddDelegate), Unbind (RemoveDelegate), Clear
- Animation Blueprint property access (fast path)
- Reflection-based dispatch: any function call with an argument pin named `PropertyName`, `VariableName`, or `FieldName` and a literal string or name default value. Catches `MarkPropertyDirty`, Dataflow variable overrides, and user helpers.
- Any custom K2Node that implements `UK2Node::ReferencesVariable`

**Config:**

- `IgnoredNames`: explicit list of variable names to skip. Use for variables accessed by C++ parent classes or other systems the static analyzer cannot follow.
- `IgnoredPrefixes`: skip variables whose name starts with any of these prefixes. Case-insensitive.

## Naming Convention

| | |
|---|---|
| **Rule ID** | NamingConvention |
| **Severity** | Info |

Checks multiple naming convention violations:

- Boolean variables must start with lowercase **b** (e.g., bIsReady, bCanFire)
- The character after **b** must be uppercase (e.g., bReady, not bready)
- Non-boolean variables must start with uppercase (PascalCase)
- Variables and functions must not contain spaces
- Variables and functions must not contain non-ASCII characters
- Functions must start with uppercase (PascalCase)

## Missing Description

| | |
|---|---|
| **Rule ID** | MissingDescription |
| **Severity** | Info |

Functions without a tooltip or description. Adding descriptions helps team members understand what each function does without reading its implementation.

Skips the default UserConstructionScript graph.

## Uncategorized Variables

| | |
|---|---|
| **Rule ID** | UncategorizedVariables |
| **Severity** | Info |

Instance Editable (public) variables without a Category set. When actors are placed in levels, uncategorized variables clutter the Details panel.

Only checks variables with Instance Editable enabled.

## TODO Comments

| | |
|---|---|
| **Rule ID** | TodoComments |
| **Severity** | Info |

Comment nodes containing TODO, FIXME, HACK, or TEMP (case insensitive). A reminder of unfinished work that should be addressed.

## Empty Functions

| | |
|---|---|
| **Rule ID** | EmptyFunction |
| **Severity** | Info |

Function graphs with no meaningful nodes (only the entry node). These should be either implemented or removed.

Skips the default UserConstructionScript graph.

## Unused Functions

| | |
|---|---|
| **Rule ID** | UnusedFunction |
| **Severity** | Warning |

Functions **and Custom Events** defined in the Blueprint but never called from any graph within the same Blueprint.

RPC functions (Server/Client/Multicast) are **not** auto-skipped. An RPC that nobody invokes is dead code just like any other function -- the networking layer only dispatches the body, the call must still originate somewhere. If an RPC is invoked cross-Blueprint or from a C++ parent, add it to `IgnoredNames`.

**Functions -- automatically skipped:**

- Parent class overrides (e.g. `GetLifetimeReplicatedProps`, `OnConstruction`)
- Blueprint interface implementations
- Exec functions -- invoked from the console
- Functions matching the `AnimNotify_` convention -- dispatched by animation assets
- Functions bound via "Create Event" nodes (the `K2Node_CreateDelegate` path used when binding a regular function to a multicast delegate)
- Functions referenced by name in the `Set Timer by Function Name` family, and any user helper that takes a `FunctionName`, `FuncName`, or `EventName` string parameter

**Custom Events -- automatically skipped:**

- Custom events overriding a custom event declared in a parent Blueprint
- Custom events implementing an interface event
- Custom events whose name matches a parent C++ `BlueprintImplementableEvent`
- Exec custom events
- Custom events matching the `AnimNotify_` convention
- Custom events whose `OutputDelegate` pin is wired into a Bind Event / Assign / AddDelegate node (direct delegate binding -- no intermediate Create Event node is generated for this pattern, so it needs its own check)

**Config:**

- `IgnoredNames`: explicit list of function/event names to skip. Use for callbacks bound from C++ parent classes and for RPCs called cross-Blueprint.
- `IgnoredPrefixes`: skip names starting with any of these prefixes. Case-insensitive.
