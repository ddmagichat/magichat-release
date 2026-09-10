# Tasks and Tools

Task Center runs reusable scripts as managed tasks, while the Tools page provides focused utilities for common desktop workflows.

## Create a script task

1. Open **Task Center**.
2. Start creating a script task.
3. Enter a clear task name.
4. Select PowerShell, CMD, Node.js, or Python as the script type.
5. Enter the script content.
6. Add values for any Macros used by the script.
7. Review the resume option and other available task settings.
8. Create the task.

A task appears in the Active list while it is queued or running. Its row shows the script type, creation time, lifecycle status, and exit code when one is available.

## Use variables in a task

Task scripts use the same `mh{key}` Macro syntax as Commands. For example:

```powershell
Write-Host "Processing mh{source.path}"
Write-Host "Output directory: mh{output.path}"
```

When you add or remove Macro references in the script, review the variables shown by the task form and provide a value for every required key. Variable values can reference other variables, but references must exist and must not form a cycle.

Task variables belong to the task. They are separate from Command Folder parameters and Workspace Env.

## Save and reuse templates

Templates are useful when several tasks share the same interpreter, script, variables, or run settings.

1. Configure a task form with the script and values you want to reuse.
2. Save the form as a template.
3. Open the template when you need another task with the same starting configuration.
4. Adjust the task name or variables for the new run.
5. Create the task.

You can clone an existing template to create a variation without replacing the original.

## Monitor tasks and logs

Task Center separates tasks into Active and Complete views:

- **Active** contains queued and running tasks.
- **Complete** contains succeeded, failed, and abandoned tasks.

Expand a task to inspect its original script, variable values, and recent log output. The inline log keeps a limited recent tail for quick inspection. Use **Show log file** when you need the current log file in Windows File Explorer.

Completed tasks can be marked as viewed, sorted by time or script type, pinned, selected, or deleted using the controls available in Task Center. Use **Run new** to create another run from an existing task without editing its historical record.

## Use the Markdown tool

The Markdown tool provides a dedicated editing workspace with source and preview panes.

1. Open **Tools** and select **Markdown**.
2. Enter or paste Markdown in the source pane.
3. Review the rendered result in the preview pane.
4. Resize or collapse the panes when you need more space for editing or previewing.

The preview is sanitized before rendering. It is suitable for checking documentation without treating embedded HTML as trusted application content.

## Find which process is using a file

Use File Occupancy when Windows reports that a file is open in another program:

1. Open **Tools** and select **File Occupancy**.
2. Choose or enter the file you want to inspect.
3. Start the query.
4. Review the matching process names and identities.

If you choose to terminate a process from the result list, first confirm that it is safe to stop. Ending a process can discard unsaved work or interrupt another application.

## Related guides

- [Getting Started](getting-started.md)
- [Commands and Macros](commands-and-macros.md)
- [Back to the MagicHat README](../README.md)
