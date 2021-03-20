

# Documenting Your Commands

During an engagement, one can easily forget to document the commands that were executed.  
Luckily, PowerShell has a cmdlet that will document which commands are used and include the time they were executed.

<br>

####PowerShell cmdlet to start logging commands
- Start-Transcript

<br>

####PowerShell cmdlet to stop logging commands
- Stop-Transcript

<br>

####Example
- <code>Start-Transcript -Path "C:\temp\PSlog.txt" -IncludeInvocationHeader</code>
- The -Path parameter is where you want to save the log
- The -IncludeInvocationHeader is an important parameter to include because this will document the time each command is executed 

<br>

###PowerShell Transcript Exercise

<br>

Enter <code>Start-Transcript -Path "C:\temp\PSlog.txt" -IncludeInvocationHeader</code> into the PowerShell terminal

![](screenshots/ps_snip13.png)

Type a few random commands into the terminal

![](screenshots/ps_snip14.png)

Enter the <code>Stop-Transcript</code> cmdlet to stop transcribing

![](screenshots/ps_snip16.png)

Type <code>Get-Content -Path "C:\temp\PSlog.txt"</code> to view the command log that you created

![](screenshots/ps_snip15.png)






 


















