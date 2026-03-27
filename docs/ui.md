# UI Overview

## Toolbar

| Button | Action |
|--------|--------|
| **Scan All** | Scans every Blueprint under /Game |
| **Scan Directory...** | Opens a folder picker to scan a specific directory |
| **Scan Selected** | Scans whatever is selected in Content Browser (assets or folders) |
| **Export JSON** | Saves results to a JSON file |
| **Clear** | Clears current results |

## Filters

### Text Filter
Type in the search box to filter results by Blueprint name, rule name, category, graph name, or message text.

### Severity Toggles
Three checkboxes with counts: **ERR**, **WRN**, **INF**. Toggle each to show or hide violations of that severity level.

### Rules Dropdown
Click the **Rules** button to open a dropdown with checkboxes for each rule that has violations. Shows violation count per rule. Use **All** / **None** buttons to quickly toggle all rules.

## Sorting

Click any column header to sort by that column:
- **Sev**: severity level
- **Category**: rule category
- **Blueprint**: Blueprint name
- **Graph**: graph name
- **Message**: violation message

Click the same header again to reverse the sort direction.

## Navigation

- **Double-click** any row to open the Blueprint Editor and focus on the problem node
- Click the **>>** button on the right side of each row for the same effect
- If the specific node is no longer available, the Blueprint itself opens
