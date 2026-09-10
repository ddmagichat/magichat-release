# Commands and Macros

The Command page turns scripts you use repeatedly into organized, parameterized Command Items with their own terminals.

## Understand the Command hierarchy

MagicHat organizes Command data into four levels:

1. A **Root** is an absolute directory that contains one or more Workspaces.
2. A **Workspace** is a top-level directory inside the selected Root.
3. A **Folder** groups related Commands and can provide shared parameters.
4. A **Command Item** stores a script type, script content, parameter groups, and the selected parameter group.

Only one Root is active at a time. The built-in `default` Root cannot be edited or removed. You can add other Roots from the Command page settings when you want to keep separate collections of Workspaces.

## Create a parameterized Command

1. Open the **Command** page and select a Workspace.
2. Create a Folder named `build`.
3. Create a Command Item inside it named `build project`.
4. Select **PowerShell** as the script type.
5. Add these parameters to the Item's active parameter group:

| Key | Example value |
| --- | --- |
| `project.name` | `SampleApp` |
| `build.mode` | `Release` |
| `output.path` | `D:\Build Output` |

6. Enter this script:

```powershell
Write-Host "Project: mh{project.name}"
Write-Host "Mode: mh{build.mode}"
Write-Host "Output: mh{output.path}"
```

7. Save and run the Item.

MagicHat replaces each Macro before the script is sent to the Terminal.

## Use Macro scopes

A Macro uses the syntax `mh{key}`. Keys start with a letter or underscore and may contain letters, numbers, underscores, dots, and hyphens.

When the same key exists in multiple places, MagicHat applies this priority from highest to lowest:

1. Workspace Env
2. The active parameter group on the Command Item
3. Parent Folder parameter groups, from the nearest Folder outward

Use Folder parameters for values shared by several Commands. Use Item parameters for Command-specific values. Use Workspace Env for values that should override Commands throughout the current Workspace.

Disabled parameters do not participate in Macro resolution. Parameter values may reference other Macros, but references must exist and must not form a cycle.

## Maintain multiple parameter groups

A Command Item can store multiple named parameter groups. For example, a deployment Command could have `Development`, `Staging`, and `Production` groups with different targets.

Before running the Command:

1. Open its parameter section.
2. Select the required group.
3. Review the resolved values.
4. Save the Item if the selection or values changed.
5. Run the Command.

This keeps the script itself unchanged while making the execution context explicit.

## Update Workspace Env from a script

Scripts launched by a MagicHat Terminal can call `mhsetenv` to persist values in the current Workspace Env.

PowerShell:

```powershell
mhsetenv "BUILD_MODE" "release" "OUTPUT_DIR" "D:\Build Output"
```

Node.js:

```javascript
mhsetenv({
  BUILD_MODE: "release",
  OUTPUT_DIR: "D:\\Build Output",
});
```

Python:

```python
mhsetenv({
    "BUILD_MODE": "release",
    "OUTPUT_DIR": r"D:\Build Output",
})
```

CMD:

```bat
call mhsetenv "BUILD_MODE" "release" "OUTPUT_DIR" "D:\Build Output"
```

Later Commands can read these values as `mh{BUILD_MODE}` and `mh{OUTPUT_DIR}`. In CMD scripts, keep the `call` prefix so control returns to the current batch script.

## Call another saved Command

Use `mhcall` when one Command needs to synchronously run another saved Command Item:

```powershell
mhcall("default/tools/build project")
```

The path must include the Workspace name and identify a saved Item, not a Folder. `mhcall` waits for the target script to finish before continuing. It uses the saved version of the target Command, so save pending edits first.

## Troubleshooting

- If a Macro is unresolved, check its spelling, enabled state, active parameter group, and scope.
- If Macro resolution reports a cycle, inspect parameter values that reference each other.
- If `mhcall` cannot find an Item, verify the Workspace-inclusive path and save the target Item.
- If a CMD helper does not return to the script, confirm that it is invoked with `call`.

## Related guides

- [Getting Started](getting-started.md)
- [Tasks and Tools](tasks-and-tools.md)
- [Back to the MagicHat README](../README.md)
