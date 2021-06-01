

# Performing a Directory Walk 

<br>
There are multiple methods that you can use to perform a directory walk.  It is important to note that trying to perform this task remotely can take significant time.  There are two ways that this process can be made much faster.  The first is to save the output from the command to a file on the remote system and then pull the file back after completion.  The second, is to use the .NET class [System.IO.Directory] which only pulls the file name, however it is 1000x faster than using Get-ChildItem.

####Commands

- <code>Get-ChildItem -Path C:\ -Recurse -Force</code>
- <code>[System.IO.Directory]::EnumerateFiles($path,'*.*','AllDirectories')</code>

<br>

####Examples
  
    #Examples for using GCI
    Get-ChildItem -Path C:\ -Recurse -Force | Select-Object FullName, Name, LastWriteTime

    Get-ChildItem -Path $startPath -Recurse | Where-Object {$_.LastWriteTime -gt (Get-Date).addDays(-30) -or $_.CreationTime -gt (Get-Date).addDays(-30)}

    #Example using the .NET class
    $path = 'C:\'
    $files = [System.IO.Directory]::EnumerateFiles($path,'*.*','AllDirectories')







