# Problem

When running `/?` or `--help` for some commands, it's difficult to read through the output. It would be better to launch this output in Notepad (or other editor) to read and search through the output.  

# Solution

A simple script in batch file can do this via PowerShell. It passes output of the command line program to the clipboard and then launches Notepad and pastes the output there.  

```cmd
@echo off
clip
powershell -Command $process = Start-Process -PassThru notepad;$SW_SHOW = 5;$sig = '[DllImport("""user32.dll""")] public static extern bool ShowWindow(IntPtr hWnd, int nCmdShow);';Add-Type -MemberDefinition $sig -name NativeMethods -namespace Win32;[Win32.NativeMethods]::ShowWindow($process.Id, $SW_SHOW) ^| Out-Null;Add-Type -AssemblyName System.Windows.Forms;[System.Windows.Forms.SendKeys]::SendWait('^^V');
```

[Source from SuperUser](https://superuser.com/a/772751/96992)