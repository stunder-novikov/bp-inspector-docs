# Style & Organization Rules

## Unused Variables

| | |
|---|---|
| **Rule ID** | UnusedVariables |
| **Severity** | Warning |

Variables declared in the Blueprint but never referenced (no Get or Set nodes) in any graph.

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

Functions defined in the Blueprint but never called from any graph within the same Blueprint.

Functions that override parent class methods are skipped.
