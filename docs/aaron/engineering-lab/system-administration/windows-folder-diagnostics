# Windows Folder Diagnostics

## Overview

Sometimes Windows Explorer appears to lose a folder.

Before assuming the folder is deleted or corrupted, verify each layer of the system.

This workflow focuses on:

- Folder existence
- Folder attributes
- Windows known-folder configuration
- Visibility issues

---

# Diagnostic Model

```text
                 USER REPORT

              "Folder Missing"

                     |
                     v

              APPLICATION LAYER

       Can programs still access it?

                     |
                     v

              FILE SYSTEM LAYER

          Does the folder exist?

                     |
                     v

              ATTRIBUTE LAYER

        Is it hidden or protected?

                     |
                     v

           WINDOWS CONFIGURATION

       Is Windows pointing correctly?

                     |
                     v

                 RESOLUTION
```

---

# Case Study — Missing Downloads Folder

## Symptom

Downloads was available inside Brave Browser but missing from Windows Explorer.

This indicated:

- The folder probably existed.
- The issue was likely visibility or configuration.

---

# Step 1 — Verify User Profile Location

Command:

```powershell
[Environment]::GetFolderPath("UserProfile")
```

Example:

```text
C:\Users\aaron
```

Purpose:

Confirms the active Windows profile location.

---

# Step 2 — Search Hidden Files and Folders

Command:

```powershell
dir C:\Users\aaron -Force
```

## Why Use `-Force`?

Normal Explorer views hide:

- Hidden folders
- System folders

The `-Force` parameter reveals them.

Example:

```text
Downloads
```

Finding the folder confirms:

✅ Folder exists
✅ Data was not lost

---

# Step 3 — Inspect Folder Attributes

Command:

```powershell
Get-Item C:\Users\aaron\Downloads | Format-List *
```

Important field:

```text
Attributes
```

Example:

```text
Attributes : ReadOnly, Directory, Archive, NotContentIndexed
```

---

# Attribute Explanation

| Attribute | Meaning |
|-|-|
| Directory | Object is a folder |
| Hidden | Explorer hides the folder |
| ReadOnly | Normal folder metadata flag |
| Archive | Used by backup systems |
| NotContentIndexed | Windows Search ignores contents |

---

# Step 4 — Verify Windows Folder Mapping

Windows stores known-folder locations in the registry.

Command:

```powershell
reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders"
```

Find:

```text
{374DE290-123F-4565-9164-39C4925E467B}
```

This GUID represents Downloads.

Expected:

```text
%USERPROFILE%\Downloads
```

---

# Step 5 — Remove Hidden Attribute

If the folder is hidden:

Command:

```powershell
attrib -h C:\Users\aaron\Downloads
```

Restart Explorer:

```powershell
taskkill /f /im explorer.exe
start explorer.exe
```

---

# Final Diagnosis Example

## Problem

```text
Downloads missing from Windows Explorer
```

---

## Investigation

```text
Browser Access
        |
        v
Folder Exists

        |
        v

File System Check

        |
        v

Hidden Attribute Found

        |
        v

Hidden Attribute Removed

        |
        v

Explorer Restored
```

---

# Troubleshooting Philosophy

Avoid immediately:

- Reinstalling Windows
- Editing random registry values
- Restoring backups unnecessarily

Instead:

1. Observe the problem.
2. Collect evidence.
3. Identify the failed layer.
4. Change only the affected component.

Good troubleshooting is controlled experimentation.