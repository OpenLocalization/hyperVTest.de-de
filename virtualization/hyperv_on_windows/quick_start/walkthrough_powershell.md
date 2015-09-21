MS. ContentId: B9414110-BEFD-423F-9AD8-AFD5EE612CDA
Titel: Schritt 8: Experimentieren Sie mit WindowsPowerShell

#Schritt 8: Experimentieren Sie mit WindowsPowerShell

Nun, da Sie die Grundlagen der Bereitstellung von Hyper-V, virtuelle Computer erstellen und verwalten diese virtuellen Computer durchlaufen haben, betrachten wir wie diesen Aktivitäten mit PowerShell automatisiert werden können.

###Zurückgeben einer Liste von Hyper-V-Befehle

1.  Klicken Sie auf die Windows-Start-Taste, Typ **PowerShell**.
2.  Führen Sie den folgenden Befehl aus, um eine durchsuchbare Liste mit PowerShell-Befehle zur Verfügung, mit dem Hyper-V-PowerShell-Modul anzuzeigen.
    
    '''Powershell
    Get-Command – Modul hyper-V | Out-gridview


```
  You get something like this:

  ![](media\command_grid.png)

3. To learn more about a particular PowerShell command use `get-help`. For instance running the following command will return information about the `get-vm` Hyper-V command.

  ```powershell
get-help get-vm

```

 Die Ausgabe veranschaulicht die Struktur des Befehls, was die erforderlichen und optionalen Parameter sind und die Aliase, die Sie verwenden können.

!(media\get_help.png)

###Zurückgeben einer Liste von virtuellen Computern

Verwenden Sie das `get-vm` Befehl, um eine Liste von virtuellen Computern.

1.  Führen Sie in PowerShell den folgenden Befehl ein:
    
    `powershell
    get-vm
    `
    Etwa wie folgt angezeigt:
    
    !(media\get_vm.png)
2.  Zurückzugebenden eine Liste nur virtuelle Computer eingeschaltet hinzufügen einen Filter, um die `get-vm` -Befehl abgerufen wird.
    Ein Filter kann hinzugefügt werden, mit dem Where-Object-Befehl.
    Weitere Informationen zum Filtern finden Sie unter der [Die Where-Object verwenden](https://technet.microsoft.com/en-us/library/ee177028.aspx) Dokumentation.
    
    '''Powershell
    Get-Vm | wobei {$_. Status – Eq 'Running'}


 ```
3.  To list all virtual machines in a powered off state, run the following command. This command is a copy of the command from step 2 with the filter changed from ‘Running’ to ‘Off’.

 ```powershell
 get-vm | where {$_.State –eq ‘Off’}

 ```


###Starten und Herunterfahren von virtuellen Maschinen

1.  Um einen bestimmten virtuellen Computer zu starten, führen Sie den folgenden Befehl mit dem Namen des virtuellen Computers:
    
    '''Powershell
    Start-Vm-Name < Name des virtuellen Computers >


 ```

2. To start all currently powered off virtual machines, get a list of those machines and pipe the list to the 'start-vm' command:

  ```powershell
 get-vm | where {$_.State –eq ‘Off’} | start-vm

 ```

1.  Um alle ausgeführten virtuellen Computer herunterzufahren, führen Sie dies:
    
    '''Powershell
    Get-Vm | wobei {$_. Status – Eq 'Running'} | Stop-vm


 ```

### Create a VM checkpoint

To create a checkpoint using PowerShell, select the virtual machine using the `get-vm` command and pipe this to the `checkpoint-vm` command. Finally give the checkpoint a name using `-snapshotname`. The complete command will look like the following:

 ```powershell
 get-vm -Name <VM Name> | checkpoint-vm -snapshotname <name for snapshot>

 ```

Hier ist z. B. ein Prüfpunkt mit dem Namen DEMOCP:

!(media\POSH_CP2.png)

###Erstellen eines neuen virtuellen Computers

Das folgende Beispiel zeigt, wie Sie einen neuen virtuellen Computer in die PowerShell Integrated Scripting Environment (ISE) erstellen.
Dies ist ein einfaches Beispiel und weitere PowerShell-Funktionen und erweiterte VM-Bereitstellungen auf erweitert werden konnte.

1.  Geben Sie zum Öffnen der PowerShell ISE klicken Sie auf "Start" **PowerShell ISE**.
2.  Führen Sie den folgenden Code zum Erstellen eines virtuellen Computers.
    Finden Sie in der [New-VM](https://technet.microsoft.com/en-us/library/hh848537.aspx) Dokumentation für ausführliche Informationen zu den New-VM-Befehl.
    
    '''Powershell
    $VMName = "VMNAME"
    
    $VM = @ {}
     Name = $VMName 
     MemoryStartupBytes = 2147483648
     Generation = 2
     NewVHDPath = "C:\Virtual Machines\$VMName\$VMName.vhdx"
     NewVHDSizeBytes = 53687091200
     BootDevice = "VHD"
     Path = "C:\Virtual Machines\$ VMName"
     SwitchName = (Get-Vmswitch). Name [0]
    }
    
    Neue VM @VM
    ```

##Wrappen und Verweise

Dieses Dokument hat einige einfache Schritte zum Explorer das Hyper-V-PowerShell-Modul sowie einige Beispielszenarios gezeigt.
Weitere Informationen über die Hyper-V-PowerShell-Modul, finden Sie unter der [Hyper-V-Cmdlets in Windows PowerShell-Referenz](https://technet.microsoft.com/%5Clibrary/Hh848559.aspx).


