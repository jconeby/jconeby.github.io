

# Performing a Directory Walk 

####Commands

- Get-ChildItem -Path C:\ -Recurse -Force
- [System.IO.Directory]::EnumerateFiles($path,'*.*','AllDirectories')

<br>

####Examples

- Get-ChildItem -Path C:\ -Recurse -Force | Select-Object FullName, Name, LastWriteTime

- Get-ChildItem -Path $startPath -Recurse | Where-Object {$_.LastWriteTime -gt (Get-Date).addDays(-30) -or $_.CreationTime -gt (Get-Date).addDays(-30)}

















