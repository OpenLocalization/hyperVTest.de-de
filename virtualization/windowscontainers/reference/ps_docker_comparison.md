MS. ContentId: 4981828d-1a08-4d8c-a99d-874a926a153f
Titel: PowerShell Docker Vergleich

#PowerShell zum Vergleich der Docker für die Verwaltung von Windows Server-Container

Es gibt viele Verfahren zum Verwalten von Windows Server-Container mit integrierten Windows-Tools (in dieser Vorschau PowerShell) und Open-Source-Verwaltungstools, wie z. B. Docker.
Führungslinien Gliedern beide einzeln erhältlich hier:

*   [Verwalten von Windows Server-Container mit Docker](../quick_start/manage_docker.md)
*   [Verwalten von Windows Server-Container mit PowerShell](../quick_start/manage_powershell.md)

Diese Seite ist einem mehr Tiefe Referenz Vergleich von Docker-Tools und PowerShell-Verwaltungstools.

##PowerShell für Container im Vergleich zu Hyper-V-Computern

Erstellen können, ausführen und mit Windows Server-Container mit PowerShell-Cmdlets interagieren.
Alles, was Sie benötigen den Einstieg wird im Feld verfügbar.

Wenn Sie Hyper-V-PowerShell verwendet haben, sollte das Design der Cmdlets Recht vertraut sein.
Ein Großteil der Workflow ist ähnlich wie eine virtuelle Maschine mit dem Hyper-V-Modul verwaltet.
Anstelle von `New-VM`, `Get-VM`, `Start-VM`, `Stop-VM`, Sie haben `New-Container`, `Get-Container`, `Start-Container`, `Stop-Container`.
Es gibt einige Container-spezifische Cmdlets und Parameter, aber die allgemeine Lebenszyklus und Verwaltung von Windows-Container sieht in etwa wie eine Hyper-V-VM.

##Wie Vergleich PowerShell Management im zu Docker?

Die Container-PowerShell-Cmdlets verfügbar machen eine API, die nicht ganz identisch mit der Docker ist. die Cmdlets sind in der Regel genauer Vorgang.
Einige Befehle Docker sind unkompliziert Parallels in PowerShell:

| Docker-Befehl| PowerShell-Cmdlets|
|----|----|
| `docker ps -a`| `Get-Container`|
| `docker images`| `Get-ContainerImage`|
| `docker rm`| `Remove-Container`|
| `docker rmi`| `Remove-ContainerImage`|
| `docker create`| `New-Container`|
| `docker commit <container ID>`| `New-ContainerImage -Container <container>`|
| `docker load <tarball>`| `Import-ContainerImage <AppX package>`|
| `docker save`| `Export-ContainerImage`|
| `docker start`| `Start-Container`|
| `docker stop`| `Stop-Container`|
Die PowerShell-Cmdlets sind keine genaue perfekte Parität, und es gibt eine große Anzahl von Befehlen, die wir nicht PowerShell Ersatz für bereitstellen * (insbesondere `docker build` und `docker cp`).
Aber was Ihnen sofort auffallen möglicherweise darin, dass es kein einzelnes einzeilige Ersatz für `docker run`.

\ * Vorbehalten.

###Aber ich Docker ausführen! Was ist passiert?

Wir machen, ein paar Dinge, die eine etwas vertrauter Interaktionsmodell für Benutzer bereitstellen, die ihre PowerShell bereits vertraut sind.
Wenn Sie die Art und Weise Docker arbeitet verwendet, wird dies natürlich etwas ein Umdenken sein.

1.  Der Lebenszyklus eines Containers im PowerShell-Modell ist etwas anders.
    Im Container PowerShell-Modul wir die präzisere Vorgänge verfügbar machen `New-Container` (wodurch erstellt einen neuen Container, der beendet wurde) und `Start-Container`.
    
    Zwischen erstellen, und starten den Container, können Sie auch den Container Einstellungen konfigurieren. für TP3 ist nur anderen Konfigurationen, die wir bereitstellen möchten die Möglichkeit, die Netzwerkschnittstelle für den Container festlegen.
    verwenden die (hinzufügen/entfernen/Verbindung herstellen/trennen/Get/Set)-ContainerNetworkAdapter-Cmdlets.
2.  Derzeit kann keinen auszuführenden Befehl innerhalb des Containers auf "Start" übergeben werden. Allerdings können Sie immer noch eine interaktive PowerShell-Sitzung mit einem ausgeführten Container abrufen `Enter-PSSession -ContainerId <ID of a running container>`, und Sie können einen Befehl innerhalb einer ausgeführten Container mit ausführen `Invoke-Command -ContainerId <container id> -ScriptBlock { code to run inside the container }` oder `Invoke-Command -ContainerId <container id> -FilePath <path to script>`.  
    Beide Befehle ermöglichen das optionale `-RunAsAdministrator` Kennzeichen für hohe Privilige Aktionen.  

##Vorbehalte und bekannte Probleme

1.  Jetzt, die Container-Cmdlets haben keine Kenntnis über Container oder Bilder, die durch Docker erstellt und Docker weiß nicht, alles zu Containern und Images, die über die PowerShell erstellt.
    Wenn Sie in der Docker erstellt, mit der Docker verwalten; Wenn Sie es über PowerShell erstellt haben, können verwalten Sie sich über PowerShell.
2.  Wir haben eine ziemlich viel Arbeit, die wir tun, damit um der Endbenutzer – verbesserte Fehlermeldungen, bessere Fortschrittsberichte, ungültiges Ereigniszeichenfolgen usw. zu optimieren möchten.
    Wenn Sie eine Situation auftreten versehentlich, wo sollen Sie waren Weitere erste, oder Informationen besser, wir gerne Vorschläge zu den Foren zu senden.

##Eine schnelle runthrough

Im folgenden wird erörtert einige allgemeine Workflows.

Dabei wird vorausgesetzt, Sie ein Betriebssystemabbild-Container mit dem Namen "ServerDatacenterCore" installiert haben, und erstellt einen virtuellen Switch mit dem Namen "Virtueller Switch" (mit dem New-VMSwitch).

''' PowerShell

###1 Auflisten von Bildern

#An diesem Punkt können Sie die Bilder auf dem System auflisten:

Get-ContainerImage

#Get-ContainerImage nimmt auch filtern.

#Beispielsweise wird alle Container Bilder zurückgegeben, deren Name mit S (Groß-/Kleinschreibung) beginnt:

Get-ContainerImage-Namen S *

#Sie können die Ergebnisse dieser einer Variablen speichern.

#(Wenn Sie nicht mit PowerShell vertraut sind, kennzeichnet das "$" eine Variable.)

$baseImage = Get-ContainerImage-Namen ServerDatacenterCore
$baseImage

###2. Erstellen und Auflisten von Containern

#Jetzt können wir einen neuen Container mit diesem Abbild erstellen:

Neuen Container - Name "MyContainer" - ContainerImage $baseImage - SwitchName "Virtueller Switch"

#Jetzt können wir alle Container aufzählen.

Get-Container

#Auf ähnliche Weise speichern wir dieses Containers zu einer Variablen:

$container1 = Get-Container-Namen "MyContainer"

###3. Starten von Containern, die Interaktion mit dem Ausführen von Containern und Beenden von Containern

#Nun beginne, und starten Sie den Container.

Start-Container-Namen "MyContainer"

#(Wir könnten haben auch gestartet diesen Container mit "Start-Container-Container $container1".)

#Geben Sie mit dem Container, der ausgeführt wird eine interaktive PowerShell-Sitzung und wir:

Geben Sie-PSSession - des Elements $container1. ID

#Dadurch sollte schließlich eine Aufforderung PowerShell aus dem Container angezeigt.

#Sie können versuchen, alle Elemente, die bei der angegebenen interactive Cmd Prompt "Docker run - es".

#Jetzt können wir nur um zu beweisen, dass wir hier Waren eine neue Datei erstellen:

CD \
Mkdir Test
Test-CD
Echo "Hello World" > hello.txt
exit

#Wir sollten jetzt wieder in der Außenwelt sein. Obwohl wir die PowerShell-Sitzung beendet haben,

#der Container selbst wird weiterhin ausgeführt, wie Sie sehen können, indem Sie den Container erneut ausgeben:

$container1

#Bevor wir uns dieses Containers ein neues Abbild verpflichten können, müssen wir den Container zu beenden.

#Das machen wir jetzt.

Stop-Container - Container $container1

###4. Erstellen ein neues Container-Bild

#Und nun lassen Sie uns einen commit in ein neues Bild.

$image1 = neue ContainerImage-Container $container1-Verleger Test - Namen Image1-Version 1.0

#Zählen Sie alle Bilder erneut auf, aus Gründen der Nerven:

Get-ContainerImage

#Und wiederholen. Stellen Sie einen anderen Container basierend auf das neue Bild.

$container2 = neuen Container-Namen "MySecondContainer" - ContainerImage $image1 - SwitchName "Virtueller Switch"

#(Falls gewünscht, können Sie beginnen Sie den zweiten Container und überprüfen Sie, ob die neue Datei

#"\Test\hello.txt" gibt es erwartungsgemäß.)

###5. Entfernen eines Containers

#Der erste erstellte Container wird jetzt beendet. Entfernen Sie es:

Entfernen eines Containers-Container $container1

#Und dann ist es bestätigen:

Get-Container

###6. Exportieren, entfernen und Importieren von Bildern

#Für Bilder, die die grundlegende Betriebssystemabbild sind, können wir sie in einer Paketdatei AppX exportieren.

Export-ContainerImage-$image1 Image-Pfad "C:\exports"

#Dies sollte eine AppX-Datei im Ordner C:\exports erstellen.

#Wenn Sie Publisher, Name und Version des Abbilds gegeben haben wir bereits verwendet werden,

#erwarten Sie benannt werden, die sich ergebende AppX "CN = Test_Image1_1.0.0.0.appx".

#Bevor wir das Abbild erneut zu importieren versuchen können, müssen wir das Bild zu entfernen.

#(Wenn Sie Container ausgeführt, die von diesem Bild abhängen haben, sollten Sie zunächst beenden).

Remove-ContainerImage-Image $image1

#Jetzt sehen wir erneut importieren Sie das Bild:

Import-ContainerImage-Pfad C:\exports\CN=Test_Image1_1.0.0.0.AppX

#Wir hatten einen Container zuvor abhängig von diesem Abbild erstellt. Sie können können sie starten:

Start-Container-Container $container2 


```

### Build your own sample
You can see all the Containers cmdlets using `Get-Command -Module Containers`.  There are several other cmdlets that are not described here, which we'll leave to you to learn about on your own.    
**Note** This won't return the `Enter-PSSession` and `Invoke-Command` cmdlets, which are part of core PowerShell.

You can also get help about any cmdlet using `Get-Help [cmdlet name]`, or equivalently `[cmdlet name] -?`.  Today, the help output is auto-generated and just tells you the syntax for commands; we will be adding further documentation as we get closer to finalizing the cmdlet design.

A nicer way to discover the syntax is the PowerShell ISE, which you may not have looked at before if you haven't used PowerShell very much. If you're running on a SKU that permits it, try starting the ISE, opening the Commands pane, and choosing the "Containers" module, which will show you a graphical representation of the cmdlets and their parameter sets.

PS: Just to prove it can be done, here's a PowerShell function that composes some of the cmdlets we've seen already into an ersatz `docker run`. (To be clear, this is a proof of concept, not under active development.)

``` PowerShell
function Run-Container ([string]$ContainerImageName, [string]$Name="fancy_name", [switch]$Remove, [switch]$Interactive, [scriptblock]$Command) {
    $image = Get-ContainerImage -Name $ContainerImageName
    $container = New-Container -Name $Name -ContainerImage $image
    Start-Container $container

    if ($Interactive) {
         Start-Process powershell ("-NoExit", "-c", "Enter-PSSession -ContainerId $($container.Id)") -Wait
    } else {
        Invoke-Command -ContainerId $container.Id -ScriptBlock $Command
    }

    Stop-Container $container

    if ($Remove) {
        Remove-Container $container -Force
    }
} 

```


##Docker

Windows Server-Container können mit Docker-Befehlen verwaltet werden.
Während Windows Container ihren Gegenstücken Linux vergleichbar sein und sollte die gleiche Verwaltung über Docker auftreten, stehen einige Docker-Befehle, die einfach mit einem Windows-Container nicht sinnvoll sind.
Andere einfach noch nicht getestet wurden (wir gehen vorhanden).

In dem Bestreben, die API-Dokumentation Docker nicht duplizieren ist hier ein Link zu ihrer Verwaltungs-APIs.
Die exemplarischen Vorgehensweisen sind fantastisch.

Wir überwachen die Dinge, die funktionieren und nicht in die Docker-APIs in unser Dokument In Bearbeitung.


