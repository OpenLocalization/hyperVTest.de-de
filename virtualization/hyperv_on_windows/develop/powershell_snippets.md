MS. ContentId: 8DE9250B-556B-47BC-AD9A-8992B3D3D0F9
Titel: PowerShell-Ausschnitte

#PowerShell-Ausschnitte

Hinzufügen von diesem Satz für HO Kont Testverfahren.
PowerShell ist ein großartiger Skripting, Automatisierung und Verwaltungstool für Hyper-V.  Hier ist eine Toolbox zum Erkunden einiger neuen Dinge, die sie ausführen kann.

Alle Hyper-V-Verwaltung ausgeführt werden müssen als Administrator angenommen alle Skripts und Ausschnitte als Administrator über ein Administratorkonto mit Hyper-V ausgeführt werden müssen.

Wenn Sie nicht sicher, ob Sie die richtigen Berechtigungen verfügen, geben Sie `Get-VM` und wenn es ohne Fehler ausgeführt wird, sind Sie bereit.

##PowerShell-Direct-tools

Alle Skripts und Codeausschnitte in diesem Abschnitt wird auf den folgenden Grundlagen zu verlassen.

**Anforderungen** :  

*   PowerShell Direct.
    Windows-10-Gast und Host-Betriebssystem.

**Allgemeine Variablen** :  
`$VMName` – Dies ist eine Zeichenfolge mit der VMName.
Eine Liste der verfügbaren virtuellen Maschinen mit `Get-VM``$cred` --Anmeldeinformationen für das Gastbetriebssystem.
Kann mit gefüllt werden `$cred = Get-Credential`

###Überprüfen Sie, ob der Gast gestartet wurde

Hyper-V-Manager nicht Einblick in das Gastbetriebssystem, erhalten Sie dadurch häufig wird es schwierig herauszufinden, ob das Gastbetriebssystem gestartet wurde.

Verwenden Sie diesen Befehl zum Überprüfen, ob der Gast gestartet wurde.

''' PowerShell
Wenn ((Invoke-Command - VMName $VMName-Anmeldeinformationen $cred {"Test"}) - Ne "Test") {Write-Host "Nicht gestartet"} else {Write-Host "Booted"}


```

**Outcome**  
Prints a friendly message declaring the state of the guest OS.


### Script locking until the guest has booted

The following function waits uses the same principle to wait until PowerShell is available in the guest (meaning the OS has booted and most services are running) then returns.

``` PowerShell
function waitForPSDirect([string]$VMName, $cred){
   Write-Output "[$($VMName)]:: Waiting for PowerShell Direct (using $($cred.username))"
   while ((Invoke-Command -VMName $VMName -Credential $cred {"Test"} -ea SilentlyContinue) -ne "Test") {Sleep -Seconds 1}}

```

**Ergebnis**  
Druckt eine Meldung und sperren, bis die Verbindung mit dem virtuellen Computer erfolgreich ist.
Automatisch erfolgreich.

###Skript sperren, bis der Gast ein Netzwerk verfügt.

Mit PowerShell Direct ist es möglich, eine Verbindung mit einer PowerShell-Sitzung auf einem virtuellen Computer, bevor Sie den virtuellen Computer hat eine IP-Adresse empfangen.

''' PowerShell

#Warten von DHCP

während ((Get-NetIPAddress |?
AddressFamily - Eq IPv4 |?
IPAddress - Ne 127.0.0.1). SuffixOrigin - Ne "Dhcp") {sleep - 10 Millisekunden}
```

** Ergebnisses **
Sperren, bis eine DHCP-Lease empfangen wird.
Da dieses Skript nicht für ein bestimmtes Subnetz oder die IP-Adresse, sucht es funktioniert ganz gleich, welche Netzwerkkonfiguration verwenden Sie.
Automatisch erfolgreich.

##Verwalten von Anmeldeinformationen mit PowerShell

Hyper-V-Skripts erfordern häufig Anmeldeinformationen für eine oder mehrere virtuelle Maschinen, Hyper-V-Host oder beides.

Es gibt mehrere Methoden, die Sie dies erreichen können, bei der Arbeit mit PowerShell Direct oder standard-PowerShell-Remoting:

1.  Die erste (und einfachste) Möglichkeit ist die gleichen Anmeldeinformationen, die in den Host und Gast oder lokale und remote-Host gültig sein.
    Dies ist recht einfach, wenn Sie sich mit Ihrem Microsoft-Konto - Protokollierung sind oder wenn Sie in einer domänenumgebung.
    In diesem Szenario können Sie nur ausführen `Invoke-Command -VMName "test" {get-process}`.
2.  Lassen Sie PowerShell, die Sie zur Eingabe von Anmeldeinformationen  
    Wenn Sie Ihre Anmeldeinformationen nicht entsprechen, erhalten Sie automatisch eine administratoranmeldeaufforderung, sodass Sie die entsprechenden Anmeldeinformationen für den virtuellen Computer bereitstellen.
3.  Speichern von Anmeldeinformationen in einer Variablen für die Wiederverwendung.
    Ausführen eines einfachen Befehls wie folgt:  
    ` PowerShell
    $localCred = Get-Credential
    `
    Und dann etwa wie folgt:
    ''' PowerShell
    Invoke-Command - VMName "test" – Credential $localCred {Get-Process}


  ```
  Will mean that you only get prompted once per script/PowerShell session for your credentials.

4. Code your credentials into your scripts.  **Don't do this for any real workload or system**
 > Warning:  _Do not do this in a production system.  Do not do this with real passwords._

  You can hand craft a PSCredential object with some code like this:  
  ``` PowerShell
  $localCred = New-Object -typename System.Management.Automation.PSCredential -argumentlist "Administrator", (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) 

  ```

Bemessen unsichere- jedoch hilfreich beim Testen.
Jetzt können Sie keine Abfragen in dieser Sitzung.


