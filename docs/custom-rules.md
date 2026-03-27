# Adding Custom Rules

BP Inspector uses auto-discovery. Adding a new rule requires zero registration code.

## Steps

1. Create a new header and cpp file in your project
2. Create a class inheriting from `UBPInspectorRule`
3. Override the required methods
4. Compile. The rule appears automatically.

## Example

**MyCustomRule.h:**
```cpp
#pragma once
#include "Rules/BPInspectorRule.h"
#include "MyCustomRule.generated.h"

UCLASS()
class UMyCustomRule : public UBPInspectorRule
{
    GENERATED_BODY()
public:
    virtual FName GetRuleId() const override
    {
        return FName("MyCustomRule");
    }

    virtual FText GetDisplayName() const override
    {
        return FText::FromString("My Custom Rule");
    }

    virtual FText GetDescription() const override
    {
        return FText::FromString("Checks for something specific to my project");
    }

    virtual EBPInspectorCategory GetCategory() const override
    {
        return EBPInspectorCategory::BestPractices;
    }

    virtual void AnalyzeGraph(
        const UBlueprint* Blueprint,
        const UEdGraph* Graph,
        const FBPInspectorRuleConfig& Config,
        TArray<FBPInspectorViolation>& OutViolations) override;
};
```

**MyCustomRule.cpp:**
```cpp
#include "MyCustomRule.h"
#include "Core/BPGraphAnalyzer.h"
#include "Engine/Blueprint.h"
#include "EdGraph/EdGraph.h"

void UMyCustomRule::AnalyzeGraph(
    const UBlueprint* Blueprint,
    const UEdGraph* Graph,
    const FBPInspectorRuleConfig& Config,
    TArray<FBPInspectorViolation>& OutViolations)
{
    if (!Graph || !Blueprint) return;

    for (UEdGraphNode* Node : Graph->Nodes)
    {
        // Your check logic here
        // Use FBPGraphAnalyzer utilities for common operations
        // Use MakeViolation() to report issues
    }
}
```

## Available Utilities

The `FBPGraphAnalyzer` class provides static helper functions:

- `IsNodeTrivial(Node)`: true for comments, knots, entry/result nodes
- `CountNonTrivialNodes(Graph)`: count meaningful nodes
- `FindEntryNodes(Graph)`: find execution entry points
- `GetExecOutputPins(Node)` / `GetExecInputPins(Node)`: get exec pins
- `WalkExecFlow(StartNode, Visitor)`: walk execution flow with DFS
- `CalculateCyclomaticComplexity(EntryNode)`: measure complexity
- `CalculateMaxNestingDepth(EntryNode)`: measure nesting
- `IsBranchNode(Node)`, `IsCastNode(Node)`, `IsEventNode(Node)`: type checks
- `GetCalledFunctionName(Node)`: get function name from CallFunction nodes
- `HasAnyConnections(Node)`: check if node has any connected pins
- `FindReferencedVariables(Blueprint)`: all variable names used in graphs
- `GetDeclaredVariableNames(Blueprint)`: all declared variable names

## Per-Blueprint Rules

For rules that check the Blueprint as a whole (not per-graph):

```cpp
virtual bool IsPerGraphRule() const override { return false; }

virtual void AnalyzeBlueprint(
    const UBlueprint* Blueprint,
    const FBPInspectorRuleConfig& Config,
    TArray<FBPInspectorViolation>& OutViolations) override;
```

## Configuration

Custom rules automatically appear in Project Settings and can be configured with the same bEnabled, Severity, and Thresholds system as built-in rules. Override `GetDefaultThresholds()` to provide default threshold values.
