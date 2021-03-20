

# Scripting Exercise Answers

<br>

###Conditional Exercise Answer

Listed below is the answer if you decided to use an If statement

    # Save the secret word as a variable
    $secret = 'platypus'
    
    # Retrieve user input guessing the secret word
    $guess = Read-Host 'Enter the secret word'
    
    # If the user guesses the secret word display congrats message
    if ($guess -eq $secret)
    {
        Write-Output 'Congrats! You guessed the secret word'
    }
    else
    {
        Write-Output 'Sorry, better luck next time'
    }

<br>

Below is the answer if you used a Switch statement

    # Save the secret word as a variable
    $secret = 'platypus'
    
    # Retrieve user input guessing the secret word
    $guess = Read-Host 'Enter the secret word'
    
    # If the user guesses the secret word display congrats message
    switch ( $guess )
    {
        'platypus'
        {
            Write-Output 'Congrats! You guessed the secret word'
        }
        default
        {
           Write-Output 'Sorry, better luck next time'
        }
    }

<br>

###Array Exercise Answer

    # Creates an array containing the name of 3 operating systems
    $OS = @('Fedora','Windows 7','OS X Yosemite')
    
    # Returns the first item in the array
    Write-Output $OS[0]
    
    # Changes the last item in the array
    $OS[-1] = 'OS X Lion’
    
    # Adds an item to the array
    $OS += 'CentOS’
    
    # View the methods of the array object
    Get-Member -InputObject $OS
    
    # Removes the first item in the array
    $OS = $OS[1..($OS.Length-1)]

<br>

###ArrayList Exercise Answer

    # Create an arraylist of animals
    $animalFarm = [System.Collections.ArrayList]@('horse','cow','goat','pig')
    
    # Add an animal to the arraylist
    $animalFarm.Add('dog’)
    
    # Remove a specific item from the arraylist
    $animalFarm.Remove('cow')

<br>

###Tuple Exercise Answer

    # Creates a tuple containing various numbers
    $tuple = [System.Tuple]::Create(1,2,3,4,5)
    
    # Requests that the user guesses the first item in the tuple
    $numberGuess = Read-Host "What is the value of Item 1?“
    
    # Returns true or false based on correctness of guess
    $numberGuess -eq $tuple.Item1

<br>

###Hash Table Exercise Answer

    # Look at properties available
    Get-CimInstance Win32_Process | Get-Member
    
    # Select the Name, ProcessID, and ParentProcessID properties
    Get-CimInstance Win32_Process | Select Name, ProcessID, ParentProcessId
    
    # Use a hash table to selec the parent process name
    Get-CimInstance Win32_Process | Select Name, ProcessID, @{N='ParentProcessName';e={(Get-Process -Id $_.ParentProcessId).Name}}, ParentProcessId
    
    # Sort by Process ID
    Get-CimInstance Win32_Process | 
    Select Name, ProcessID, @{N='ParentProcessName';e={(Get-Process -Id $_.ParentProcessId).Name}}, ParentProcessId | 
    Sort-Object ProcessID

<br>

###Classes Exercise Answer

    class Machine {
        # Properties
        $COMPUTERNAME = $env:COMPUTERNAME
        $IP = (Get-NetIPAddress -AddressFamily IPv4).IPAddress
        $SystemInfo = (Get-ComputerInfo)
        $ProcessorArchitecture = $env:PROCESSOR_ARCHITECTURE
        $Processes = (Get-CimInstance Win32_Process)
        $Services = (Get-CimInstance Win32_Service)
        $CaptureTime = (Get-Date)
    
        # Restart Method
        Restart() {
            Restart-Computer -ComputerName $this.COMPUTERNAME -Confirm
            }
    
        # Update Capture Time Method
        UpdateCaptureTime() {
            $this.CaptureTime = Get-Date
        }
    }
    
    # Create a new instance of a Machine object
    $myMachine = [Machine]::New()
    
    # Review the properites and methods of the object
    $myMachine | GM
    
    # Update the capture time property
    $myMachine.UpdateCaptureTime()
    
    # View the object
    $myMachine

<br>

###PSCustomObject Exercise Answer

    # Run the Get-NetTCP cmdlet
    Get-NetTCPConnection
    
    # Save the established connections to a variable
    $connections = Get-NetTCPConnection -State Established
    
    # Use a foreach loop to create a PSCustomObject for each connection
    $connectionList = foreach ($connect in $connections)
    {
        [PSCustomObject]@{
            LocalAddress  = $connect.LocalAddress
            LocalPort     = $connect.LocalPort
            RemoteAddress = $connect.RemoteAddress
            RemotePort    = $connect.RemotePort
            OwningProcessID = $connect.OwningProcess
            OwningProcessName = (Get-Process -ID $connect.OwningProcess).Name
        }
    }
    
    # Format as a table
    $connectionList | FT

<br>

###Do/While Loop Exercise Answer

    # Print the even numbers from 1 to 100
    $x = 0
    
    do
    {
      if ($x % 2 -eq 0)
      {
         Write-Output $x 
      }
      $x++  
    }
    while ($x -lt 101)

<br>

###ForEach Loop Exercise Answer
    
    # Create an array containg names of zoo animals
    $zoo = @('elephant','hippo','zebra','alligator','lion','tiger','bear’)
    
    # Print each item in the array in upper case
    ForEach ($animal in $zoo) {Write-Output $animal.ToUpper()} 

<br>

###For Loop Exercise Answer

    # Print the odd numbers from 1 to 100
    for($x=0;$x -lt 100;$x++)
    {
        if($x % 2 -ne 0) {Write-Output $x}
    }

<br>


###ForEach-Object Exercise Answer

    # Animal Class
    class Animal {
        # Properties
        [string]$species
    
        # Constructor
        Animal(
          [string]$species
          
       ){
          $this.species = $species
        }
    
        # Speak Method
        Speak() 
        {
         Write-Host ('Hello I am a ' + $this.species)
        }
    }

    $animals = @('elephant','hippo','zebra','alligator','lion','tiger','bear’) 
    
    # Create a new array of animal objects using the $animals array
    $zoo = $animals | ForEach-Object {[Animal]::new($_)}
    
    # Have each object within the $zoo array invoke its Speak method
    $zoo | ForEach-Object {$_.Speak()}

<br>

###Functions Exercise Answer
    
    # Returns whether an integer is odd or even
    function Show-OddEven
    {
    Param([Parameter(Mandatory=$True)][Int32]$int)
    
      if($int % 2 -eq 0) {return ('Even')}
      return ('Odd')
         
    }