# Code Quality Rules

## Cyclomatic Complexity

| | |
|---|---|
| **Rule ID** | CyclomaticComplexity |
| **Severity** | Warning |
| **Threshold** | MaxComplexity = 10 |

Counts the number of decision points (Branch, Switch nodes) in each execution flow. Higher complexity means more paths to test and harder to understand.

**Fix:** Extract complex logic into sub-functions.

## Function Node Count

| | |
|---|---|
| **Rule ID** | FunctionNodeCount |
| **Severity** | Warning |
| **Threshold** | MaxNodeCount = 50 |

Counts non-trivial nodes in each graph. Too many nodes means the function is doing too much.

**Fix:** Split large functions into smaller, focused ones.

## Nesting Depth

| | |
|---|---|
| **Rule ID** | NestingDepth |
| **Severity** | Warning |
| **Threshold** | MaxNestingDepth = 4 |

Measures how deeply Branch nodes are nested inside each other.

**Fix:** Use early returns or extract nested logic into functions.

## Spaghetti Score

| | |
|---|---|
| **Rule ID** | SpaghettiScore |
| **Severity** | Warning |
| **Threshold** | MaxSpaghettiScore = 100 |

Composite metric combining node count, connection count, cyclomatic complexity, and nesting depth into a single number representing overall graph messiness.

## Large Blueprint

| | |
|---|---|
| **Rule ID** | LargeBlueprint |
| **Severity** | Warning |
| **Threshold** | MaxTotalNodes = 200 |

Counts total non-trivial nodes across all graphs in a Blueprint. Even if individual functions are small, the Blueprint as a whole may need to be split.

**Fix:** Split into components or child Blueprints.

## Too Many Parameters

| | |
|---|---|
| **Rule ID** | TooManyParameters |
| **Severity** | Info |
| **Threshold** | MaxParameters = 6 |

Checks the number of input parameters on functions. Too many parameters make functions hard to use and understand.

**Fix:** Group related parameters into a struct.

## Long Exec Chain

| | |
|---|---|
| **Rule ID** | LongExecChain |
| **Severity** | Info |
| **Threshold** | MaxChainLength = 20 |

Detects long linear chains of sequential nodes without branching. Long chains should be extracted into named functions for readability.
