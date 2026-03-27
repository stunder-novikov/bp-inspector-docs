# Integrations

## Content Browser

Right-click any Blueprint asset or folder in the Content Browser and select **Inspect with BP Inspector**. The BP Inspector window opens automatically with results.

Works with:
- Individual Blueprint assets
- Multiple selected assets
- Folders (scans all Blueprints inside recursively)

## Blueprint Editor Toolbar

When a Blueprint is open in the Blueprint Editor, an **Inspect** button appears in the toolbar. Click it to scan that specific Blueprint. Results appear in the BP Inspector window.

## Data Validation (Save-Time Checks)

BP Inspector integrates with Unreal's built-in Data Validation system. When enabled:

- Rules run automatically when you save a Blueprint
- Violations appear in the **Message Log**
- Click the asset name to open the Blueprint
- Click **Go To Node** to navigate directly to the problem node

To toggle: **Project Settings > Plugins > BP Inspector > Enable Data Validation**
