# Project Settings

Open **Project Settings > Plugins > BP Inspector** to configure the plugin.

## General

| Setting | Default | Description |
|---------|---------|-------------|
| **Enable Data Validation** | true | Run rules automatically when saving Blueprints |
| **Excluded Directories** | (empty) | Content paths to skip during scans (e.g., /Game/ThirdParty/) |

## Per-Rule Configuration

The **Rule Configs** map allows customizing each rule individually. Add an entry with the Rule ID as the key.

Each entry has:
- **bEnabled**: enable or disable the rule (default: true)
- **Severity**: override severity: Info, Warning, or Error
- **Thresholds**: map of threshold names to values (rule-specific)
- **IgnoredNames**: list of exact names the rule should skip. Interpretation depends on the rule (e.g. for UnusedFunction, UnusedVariables, and UnboundDispatcher this is the set of function/variable/dispatcher names that will not be flagged). Use as an escape hatch for symbols referenced by systems the static analyzer cannot follow, such as C++ parent classes.
- **IgnoredPrefixes**: list of name prefixes to skip. Case-insensitive. Useful for convention-based exclusions like `Internal_` or `BP_`.

### Threshold Reference

| Rule ID | Threshold Key | Default Value |
|---------|--------------|---------------|
| CyclomaticComplexity | MaxComplexity | 10 |
| FunctionNodeCount | MaxNodeCount | 50 |
| NestingDepth | MaxNestingDepth | 4 |
| SpaghettiScore | MaxSpaghettiScore | 100 |
| LargeBlueprint | MaxTotalNodes | 200 |
| TooManyParameters | MaxParameters | 6 |
| LongExecChain | MaxChainLength | 20 |
| TickNodeCount | MaxTickNodes | 15 |
| ConstructionScriptComplexity | MaxConstructionCC | 5 |
| ConstructionScriptComplexity | MaxConstructionNodes | 30 |

Rules without thresholds listed here are simple checks with no configurable values. You can still enable/disable them and change their severity.

If a rule is not in the Rule Configs map, it uses default settings.
