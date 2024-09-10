#  Register-ScheduledJob

Reference

Module: [PSScheduledJob](https://learn.microsoft.com/en-us/powershell/module/psscheduledjob/?view=powershell-5.1)

Creates a scheduled job
## Syntax
```powershell
Register-ScheduledJob
        [-ScriptBlock] <ScriptBlock>
        [-Name] <String>
        [-Trigger <ScheduledJobTrigger[]>]
        [-InitializationScript <ScriptBlock>]
        [-RunAs32]
        [-Credential <PSCredential>]
        [-Authentication <AuthenticationMechanism>]
        [-ScheduledJobOption <ScheduledJobOptions>]
        [-ArgumentList <Object[]>]
        [-MaxResultCount <Int32>]
        [-RunNow]
        [-RunEvery <TimeSpan>]
        [-WhatIf]
        [-Confirm]
        [<CommonParameters>]
```
```powershell
Register-ScheduledJob
        [-FilePath] <String>
        [-Name] <String>
        [-Trigger <ScheduledJobTrigger[]>]
        [-InitializationScript <ScriptBlock>]
        [-RunAs32]
        [-Credential <PSCredential>]
        [-Authentication <AuthenticationMechanism>]
        [-ScheduledJobOption <ScheduledJobOptions>]
        [-ArgumentList <Object[]>]
        [-MaxResultCount <Int32>]
        [-RunNow]
        [-RunEvery <TimeSpan>]
        [-WhatIf]
        [-Confirm]
        [<CommonParameters>]

```
## ## Description
The `Register-ScheduledJob` cmdlet creates scheduled jobs on the local computer.

A scheduled job is a Windows PowerShell background job that can be started automatically on a one-time or recurring schedule. Scheduled jobs are stored on disk and registered in Task Scheduler. The jobs can be managed in Task Scheduler or by using the Scheduled Job cmdlets in Windows PowerShell.

When a scheduled job starts, it creates an instance of the scheduled job. Scheduled job instances are identical to Windows PowerShell background jobs, except that the results are saved on disk. Use the Job cmdlets, such as `Start-Job`, `Get-Job`, and `Receive-Job` to start, view, and get the results of the job instances.

Use `Register-ScheduledJob` to create a new scheduled job. To specify the commands that the scheduled job runs, use the **ScriptBlock** parameter. To specify a script that the job runs, use the **FilePath** parameter.

Windows PowerShell-scheduled jobs use the same job triggers and job options that Task Scheduler uses for scheduled tasks.

The **Trigger** parameter of `Register-ScheduledJob` adds one or more job triggers that start the job. The **Trigger** parameter is optional, so you can add triggers when you create the scheduled job, add job triggers later, add the **RunNow** parameter to start the job immediately, use the `Start-Job` cmdlet to start the job immediately at any time, or save the untriggered scheduled job as a template for other jobs.

The **Options** parameter lets you customize the options settings for the scheduled job. The **Options** parameter is optional, so you can set job options when you create the scheduled job or change them at any time. Because job option settings can prevent the scheduled job from running, review the job options and set them carefully.

`Register-ScheduledJob` is one of a collection of job scheduling cmdlets in the **PSScheduledJob** module that is included in Windows PowerShell.

For more information about Scheduled Jobs, see the About articles in the **PSScheduledJob** module. Import the **PSScheduledJob** module and then type: `Get-Help about_Scheduled*` or see [about_Scheduled_Jobs](https://learn.microsoft.com/en-us/powershell/module/psscheduledjob/about/about_scheduled_jobs?view=powershell-5.1).

This cmdlet was introduced in Windows PowerShell 3.0.

## Examples

### Example 1: Create a scheduled job

This example creates a scheduled job on the local computer.

```powershell
Register-ScheduledJob -Name "Archive-Scripts" -ScriptBlock {
  Get-ChildItem $HOME\*.ps1 -Recurse |
    Copy-Item -Destination "\\Server\Share\PSScriptArchive"
}
```
`Register-ScheduledJob` uses the **Name** parameter to create the `Archive-Scripts` scheduled job. The **ScriptBlock** parameter runs `Get-ChildItem` that searches the `$HOME` directory recursively for `.ps1` files. The `Copy-Item` cmdlet copies the files to a directory specified by the **Destination** parameter.

Because the scheduled job doesn't contain a trigger, it's not started automatically. You can add job triggers with `Add-JobTrigger`, use the `Start-Job` cmdlet to start the job on demand, or use the scheduled job as a template for other scheduled jobs.

### Example 2: Create a scheduled job with triggers and custom options

This example shows how to create a scheduled job that has a job trigger and custom job options.

```powershell
$O = New-ScheduledJobOption -WakeToRun -StartIfIdle -MultipleInstancePolicy Queue
$T = New-JobTrigger -Weekly -At "9:00 PM" -DaysOfWeek Monday -WeeksInterval 2
$path = "\\Srv01\Scripts\UpdateVersion.ps1"
Register-ScheduledJob -Name "UpdateVersion" -FilePath $path -ScheduledJobOption $O -Trigger $T
```
The `$O` variable stores the job option object that the `New-ScheduledJobOption` cmdlet created. The options start the scheduled job even if the computer isn't idle, wakes the computer to run the job, if necessary, and allows multiple instances of the job to run in a series.

The `$T` variable stores the result from the `New-JobTrigger` cmdlet to create job trigger that starts a job every other Monday at 9:00 PM.

The `$path` variable stores the path to the `UpdateVersion.ps1` script file.

`Register-ScheduledJob` uses the **Name** parameter to create the **UpdateVersion** scheduled job. The **FilePath** parameter uses `$path` to specify the script that the job runs. The **ScheduledJobOption** parameter uses the job options stored in `$O`. The **Trigger** parameter uses the job triggers stored in `$T`.