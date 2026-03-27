# Best Practices Rules

## Disconnected Nodes

| | |
|---|---|
| **Rule ID** | DisconnectedNodes |
| **Severity** | Warning |

Finds two types of issues:
- **Orphaned nodes:** no pins connected at all
- **Dead code:** nodes with exec pins where the exec input is not connected (the node will never execute)

Disabled nodes are skipped.

## Forgotten PrintString

| | |
|---|---|
| **Rule ID** | ForgottenPrintString |
| **Severity** | Warning |

Detects PrintString, PrintText, and PrintWarning nodes. These are debug nodes that should be removed before shipping.

## Cast Without Fail Handler

| | |
|---|---|
| **Rule ID** | CastWithoutFailHandler |
| **Severity** | Warning |

Finds Cast nodes where the "Cast Failed" exec output pin is not connected. If the cast fails at runtime, the error passes silently with no handling.

Pure casts (without exec pins) are skipped.

## Empty Event Handler

| | |
|---|---|
| **Rule ID** | EmptyEventHandler |
| **Severity** | Warning |

Event nodes (BeginPlay, Tick, ActorBeginOverlap, etc.) with nothing connected to their exec output. The event fires but does nothing.

Disabled event nodes (engine default stubs) are skipped.

## Set Timer Without Clear

| | |
|---|---|
| **Rule ID** | SetTimerWithoutClear |
| **Severity** | Warning |

The Blueprint contains SetTimer calls but no ClearTimer calls anywhere. The timer may keep running indefinitely.

## Unbound Dispatcher

| | |
|---|---|
| **Rule ID** | UnboundDispatcher |
| **Severity** | Info |

Event Dispatchers that are declared as variables but never referenced (called or bound) in any graph.

## Latent Action in Loop

| | |
|---|---|
| **Rule ID** | LatentInLoop |
| **Severity** | Error |

Delay or other latent actions inside ForEach, ForLoop, or WhileLoop. This is a common mistake. Latent actions do not pause the loop: all iterations fire immediately without waiting.

## Redundant Branch

| | |
|---|---|
| **Rule ID** | RedundantBranch |
| **Severity** | Warning |

Branch nodes where the Condition pin has no connection, using the literal default value (true or false). The branch always goes one way and can be removed.
