

# Performing a Directory Walk 

####Commands

- <code>Get-ChildItem -Path C:\ -Recurse -Force</code>
- <code>[System.IO.Directory]::EnumerateFiles($path,'*.*','AllDirectories')</code>

<br>

####Examples

- Get-ChildItem -Path C:\ -Recurse -Force | Select-Object FullName, Name, LastWriteTime

- Get-ChildItem -Path $startPath -Recurse | Where-Object {$_.LastWriteTime -gt (Get-Date).addDays(-30) -or $_.CreationTime -gt (Get-Date).addDays(-30)}

















