# Getting Started with MagicHat

This guide walks you through installing MagicHat and running your first reusable command.

## Requirements

- Windows
- A supported script runtime for the commands you plan to use. PowerShell and CMD are included with Windows. Install Node.js or Python separately if your scripts require them.

## Install MagicHat

1. Open the [latest MagicHat release](https://github.com/ddmagichat/magichat-release/releases/latest).
2. Download the Windows installer.
3. Run the installer and complete the setup.
4. Launch MagicHat from the Start menu or desktop shortcut.

Only download installers published in the official `ddmagichat/magichat-release` repository.

## Create your first Command

1. Open the **Command** page.
2. Select a Workspace in the left Explorer.
3. Create a Command Item and give it a descriptive name, such as `show environment`.
4. Open the Item and select **PowerShell** as its script type.
5. Enter the following script:

```powershell
Write-Host "Hello from MagicHat"
Write-Host "Current directory: $PWD"
```

6. Save the Item.
7. Select **Run** to open its Terminal and execute the saved script.

The Terminal remains available for interactive commands after the script finishes.

## Add a reusable parameter

1. Open the parameter section of the Command Item.
2. Add a parameter named `project.name` with a value such as `MagicHat`.
3. Update the script:

```powershell
Write-Host "Building mh{project.name}"
```

4. Save and run the Item again.

MagicHat resolves `mh{project.name}` before executing the script. You can keep multiple parameter groups when the same command needs different values for different projects or environments.

## Explore the application

- Use **Task Center** for longer-running or reusable script tasks, templates, status, and logs.
- Open **Tools** for utilities such as Markdown editing and preview or File Occupancy.
- Open the page-level **Help** panel for details about the page you are currently using.

## Next steps

- [Commands and Macros](commands-and-macros.md)
- [Tasks and Tools](tasks-and-tools.md)
- [Back to the MagicHat README](../README.md)
