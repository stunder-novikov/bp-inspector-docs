# Performance Rules

## Heavy Operations in Tick

| | |
|---|---|
| **Rule ID** | HeavyOpsInTick |
| **Severity** | Warning |

Specific expensive operations called from the Tick event: GetAllActorsOfClass, line traces, GetOverlappingActors, sphere traces, box traces, and similar. These run every frame and can severely impact performance.

**Fix:** Cache results, use timers, or switch to event-driven logic.

## Unused Tick

| | |
|---|---|
| **Rule ID** | UnusedTick |
| **Severity** | Warning |

Tick event is bound and enabled but has no meaningful logic connected to its exec output. The actor ticks every frame for no reason.

**Fix:** Disable Tick in the actor's settings or Class Defaults.

## Heavy Tick

| | |
|---|---|
| **Rule ID** | TickNodeCount |
| **Severity** | Warning |
| **Threshold** | MaxTickNodes = 15 |

Counts nodes in the Tick execution flow. A heavy Tick with many nodes should be refactored into timers or event-driven logic.

## Construction Script Complexity

| | |
|---|---|
| **Rule ID** | ConstructionScriptComplexity |
| **Severity** | Warning |
| **Thresholds** | MaxConstructionCC = 5, MaxConstructionNodes = 30 |

Checks cyclomatic complexity and node count of the Construction Script with stricter thresholds than regular functions. Construction Scripts run in-editor on every property change, so they must stay lightweight.

## Expensive Construction Script

| | |
|---|---|
| **Rule ID** | ExpensiveConstructionScript |
| **Severity** | Warning |

Flags specific expensive operations inside the Construction Script: line traces, sphere traces, SpawnActor, GetAllActors, LoadAsset, and similar. These run repeatedly in the editor and can freeze it.

## GetAllActors Anywhere

| | |
|---|---|
| **Rule ID** | GetAllActorsAnywhere |
| **Severity** | Info |

GetAllActorsOfClass, GetOverlappingActors, GetAllWidgets and similar expensive operations anywhere in the Blueprint, not just in Tick.

**Fix:** Cache results in a variable if you need them multiple times.

## Nested Loops

| | |
|---|---|
| **Rule ID** | NestedForEach |
| **Severity** | Warning |

A ForEach, ForLoop, or WhileLoop nested inside another loop. This creates O(n^2) behavior that can cause significant performance issues when collections grow.

## Cast in Loop

| | |
|---|---|
| **Rule ID** | CastInLoop |
| **Severity** | Warning |

Cast nodes inside a loop body. The cast operation runs on every iteration.

**Fix:** Move the cast before the loop and store the result in a local variable.
