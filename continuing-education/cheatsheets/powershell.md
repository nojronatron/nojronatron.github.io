# Powershell Cheat Sheet

PowerShell is powerfull but I don't use it quite often enough to be an expert.

This document serves as helpful one-liners and built-ins usages that are new to me, or take me way to long to figure out (therefore this short-cut will save me time).

For the record: Gemini and Copilot have led me astray just enough times to feel the need for these quick-refs.

## Set Location to New Directory

One way:

```powershell
Set-Location -path $(New-Item -Path testing -ItemType Directory | Select-Object -Property FullName).FullName
```

Output is silent but your PWD will be the parent path plus the newly created Directory e.g. `{$_.FullName}`

Shorter, using FullName property in pipeline:

```powershell
New-Item -Path testing -ItemType Directory | Set-Location -Path {$_.FullName}
```

## Embedding Commands

According to [MSFT Documentation](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_pipelines?view=powershell-7.5#one-at-a-time-processing):

- Usually, command output can be stored in a variable to be used later
- Use parentheses to embed a command in-line using `(Get-Service)` to avoid storing `Get-Service` output in a variable
- NOTICE: PowerShell handles processing as an `IEnumerable` rather than in serial order
- NOTICE: Tabular Data is accessed through a `Rows` property

## Braces vs Brackets vs Parens

Braces `{` and `}`:

- Are __not__ executed instantly when encountered
- Define a Script Block `if ($condition) { #script block } else { #else script block}`
- Define a Function `function MyFunction { param ($Parameter1) #logic here }
- Used to indicate Enumerable (exclusive-OR options in command instructions)
- Act as a custom filter for `Where-Object`
- Used as custom property selection logic in `Select-Object`
- Define a Hash Table `$myHT = @{ Key = "Value" ...}`
- Used for handling variable names with special characters `${my spacey variable name} = "This variable has spaces"` and `Write-Host ${My spacey variable name}`

Brackets `[` and `]`:

- Retreive elements in Arrays or Hashtables
- Return items 1 through 2 in $myArray: `$myArray[1..2]`
- Select items within Hashtable $myHashtable: `$myHashtable['sd']`
- Select using RegEx-like syntax such as `Get-Service [wi]* | Select-Object Name,Status` to return only Services with names starting with 'W' or 'I'

Parens `(`and `)`:

- Exceute contained code __instantly__
- Tells PowerShell to evaluate everything inside first
- Treat it like an `Action<T>` delegate type

## References

- MSFT [PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/)
- From Patrick Gruenauer's SID-500.com [PowerShell Paraentheses Braces and Square Brackets](https://sid-500.com/2020/01/14/powershell-understanding-parentheses-braces-and-square-brackets/)

## Footer

Return to [Conted Index](../conted-index.md)
