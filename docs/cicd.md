# CI/CD Integration

## Commandlet

Run BP Inspector from the command line for automated quality gates in your build pipeline:

```
UnrealEditor-Cmd.exe YourProject.uproject -run=BPInspector -OutputFile=report.json
```

### Options

| Flag | Description |
|------|-------------|
| `-OutputFile=path.json` | Export results to a JSON file |
| `-FailOnError` | Return exit code 1 if any Error-severity violations are found |

### Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success (no errors, or -FailOnError not set) |
| 1 | Errors found (only with -FailOnError flag) |

## JSON Report Format

```json
{
  "scanTimestamp": "2026-03-27T19:10:46Z",
  "scanDurationSeconds": 0.18,
  "blueprintsScanned": 232,
  "graphsAnalyzed": 23650,
  "totalViolations": 2992,
  "violations": [
    {
      "ruleId": "CyclomaticComplexity",
      "severity": "Warning",
      "category": "CodeQuality",
      "blueprintPath": "/Game/Blueprints/BP_Enemy",
      "graphName": "EventGraph",
      "nodeName": "Branch",
      "message": "Cyclomatic complexity 14 exceeds threshold 10",
      "metricValue": 14.0,
      "thresholdValue": 10.0
    }
  ]
}
```

## Example: GitHub Actions

```yaml
- name: Run BP Inspector
  run: |
    ./UnrealEditor-Cmd.exe MyProject.uproject -run=BPInspector -OutputFile=bp_report.json -FailOnError

- name: Upload Report
  uses: actions/upload-artifact@v3
  with:
    name: bp-inspector-report
    path: bp_report.json
```
