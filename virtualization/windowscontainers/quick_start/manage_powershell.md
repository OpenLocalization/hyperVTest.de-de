MS. ContentId: d0a07897-5fd2-41a5-856d-dc8b499c6783
Titel: Verwalten von Windows Server-Container mit PowerShell

#Schnellstart: Windows Server-Container und PowerShell

In diesem Artikel werden die Grundlagen der Verwaltung von Windows Server-Container mit PowerShell durchlaufen.
Container für Windows Server und Windows Server-Container-Images erstellen, entfernen Windows Server-Container und Container Bilder und Bereitstellen einer Anwendung in einem Windows Server-Container, werden die behandelten Elemente umfassen.
Die gewonnenen Erkenntnisse in dieser exemplarischen Vorgehensweise sollten Sie zu untersuchen, Bereitstellung und Verwaltung von Windows Server-Container mit PowerShell aktivieren.

Haben Sie Fragen?
Bitten Sie sie auf der [Windows-Container-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).

> **Hinweis:** Windows Server-Container mit PowerShell erstellt können derzeit nicht mit Docker und umgekehrt verwaltet werden.
> Um Container stattdessen mit Docker zu erstellen, finden Sie unter [Schnellstart: Windows Server-Container und Docker](./manage_docker.md).
> < Br / >< Br / > Wenn Sie mehr wissen möchten, [Häufig gestellte Fragen](../about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement).
> 

##Voraussetzungen

Zum Durchführen dieser exemplarischen Vorgehensweise müssen die folgenden Elemente vorhanden sein.

*   Windows Server 2016 TP3 oder später mit dem Container-Feature von Windows Server konfiguriert.
    Wenn Sie das Handbuch abgeschlossen haben, ist dies die VM, die in Azure oder Hyper-V erstellt wurde.
*   Dieses System muss mit einem Netzwerk verbunden und auf das Internet zugreifen kann.

Wenn Sie die Container-Funktion konfigurieren müssen, finden Sie in den folgenden Handbüchern: [Container-Einrichtung in Azure](./azure_setup.md) oder [Container-Setup in Hyper-V](./container_setup.md).

##Grundlegender Container Management mit PowerShell

In diesem ersten Beispiel werden die Grundlagen zum Erstellen und Entfernen von Containern für Windows Server und Windows Server-Container-Images mit PowerShell geführt.

Die erörtert, Protokoll in Windows Server-Container Hostsystems zunächst sehen Sie eine Windows-Befehlszeile.

!(media/cmd.png)

Starten Sie PowerShell-Sitzung, indem Sie eingeben `powershell`.
Sehen Sie, dass Sie in einem PowerShell-Sitzung als die Aufforderung sind von geändert `C:\directory>` an `PS C:\directory>`.


```
C:\> powershell
Windows PowerShell
Copyright (C) 2015 Microsoft Corporation. All rights reserved.

PS C:\>

```

Verwendung `Get-Command` zum Anzeigen der verfügbaren Befehle in der Container-Modul


```
PS C:\> Get-Command -Module containers

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Function        Install-ContainerOSImage                           1.0.0.0    Containers
Function        Uninstall-ContainerOSImage                         1.0.0.0    Containers
Cmdlet          Add-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Connect-ContainerNetworkAdapter                    1.0.0.0    Containers
Cmdlet          Disconnect-ContainerNetworkAdapter                 1.0.0.0    Containers
Cmdlet          Export-ContainerImage                              1.0.0.0    Containers
Cmdlet          Get-Container                                      1.0.0.0    Containers
Cmdlet          Get-ContainerHost                                  1.0.0.0    Containers
Cmdlet          Get-ContainerImage                                 1.0.0.0    Containers
Cmdlet          Get-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Import-ContainerImage                              1.0.0.0    Containers
Cmdlet          Move-ContainerImageRepository                      1.0.0.0    Containers
Cmdlet          New-Container                                      1.0.0.0    Containers
Cmdlet          New-ContainerImage                                 1.0.0.0    Containers
Cmdlet          Remove-Container                                   1.0.0.0    Containers
Cmdlet          Remove-ContainerImage                              1.0.0.0    Containers
Cmdlet          Remove-ContainerNetworkAdapter                     1.0.0.0    Containers
Cmdlet          Set-ContainerNetworkAdapter                        1.0.0.0    Containers
Cmdlet          Start-Container                                    1.0.0.0    Containers
Cmdlet          Stop-Container                                     1.0.0.0    Containers
Cmdlet          Test-ContainerImage                                1.0.0.0    Containers

```

Im nächsten Schritt stellen Sie sicher, dass das System eine gültige IP-Adresse verwenden hat `ipconfig` ein, und notieren Sie diese Adresse für die spätere Verwendung.


```
ipconfig

Ethernet adapter Ethernet 3:

   Connection-specific DNS Suffix  . :
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb::e
   IPv6 Address. . . . . . . . . . . : 2601:600:8f01:84eb:a8c1:a3e:96b7:ffcb
   Link-local IPv6 Address . . . . . : fe80::a8c1:a3e:96b7:ffcb%5
   IPv4 Address. . . . . . . . . . . : 192.168.1.25

```

Wenn Sie statt einer Azure-VM verwenden `ipconfig` Sie müssen die öffentliche IP-Adresse der Azure-Computer zu erhalten.

!(media/newazure9.png)

###Schritt 1: Erstellen eines neuen Containers

Ein Windows Server-Container erstellt wird, müssen Sie zunächst den Namen eines Bilds Container und den Namen eines virtuellen Switches, die den neuen Container zugeordnet werden soll.

Verwenden Sie das `Get-ContainerImage` Befehl, um eine Liste der Container Bilder geladen, auf dem Host.
Notieren Sie den Namen des Abbilds, mit denen Sie den Container zu erstellen.
''' PowerShell
Get-ContainerImage

Namen Publisher Version IsOSImage
----              ---------    -------      ---------
WindowsServerCore CN = Microsoft 10.0.10514.0 True


```

Use the `Get-VMSwitch` command to return a list of switches available on the host. Take note of the switch name that will be used with the container.

``` PowerShell
Get-VMSwitch

Name           SwitchType NetAdapterInterfaceDescription
----           ---------- ------------------------------
Virtual Switch NAT

```

Führen Sie den folgenden Befehl aus, um einen Container zu erstellen.
Bei der Ausführung `New-Container` Sie benennen eines neuen Containers, angeben, welches Bild Container, und wählen Sie den Container mit den Netzwerk-Switch.
Beachten Sie dabei, dass die Ausgabe in einer Variablen $container platziert wird.
Dies wird später in dieser Übung hilfreich sein.

''' PowerShell
$container = New-Container-Name "MyContainer" - ContainerImageName WindowsServerCore - SwitchName "Virtueller Switch"


```

To see a list of containers on the host and verify that the container was created, use the `Get-Container` command. Notice that a container has been created with the name of MyContainer, however it has not been started.

``` PowerShell
Get-Container

Name        State Uptime   ParentImageName
----        ----- ------   ---------------
MyContainer Off   00:00:00 WindowsServerCore

```

Verwenden Sie zum Starten des Containers `Start-Container` Proivding den Namen des Containers.

''' PowerShell
Start-Container-Namen "MyContainer"


```

You can interact with containers using PowerShell remoting commands such as `Invoke-Command`, or `Enter-PSSession`. The example below creates a remote PowerShell session into the container using the `Enter-PSSession` command. This command needs the container id in order to create the remote session. The container id was stored in the `$container` variable when the container was created. 

Notice that once the remote session has been created the command prompt will change to include the first 11 characters of the container id `[2446380e-629]`.

``` PowerShell
Enter-PSSession -ContainerId $container.ContainerId -RunAsAdministrator

[2446380e-629]: PS C:\Windows\system32>

```

Ein Container kann sehr viel wie einen physischen oder virtuellen Computer verwaltet werden.
Befehle wie `ipconfig` die IP-Adresse des Containers zurückgeben `mkdir` zum Erstellen eines Verzeichnisses im Container und PowerShell-Befehlen wie `Get-ChildItem` alle funktionieren.
Fahren Sie fort, und nehmen Sie eine Änderung an dem Container, z. B. das Erstellen einer Datei oder eines Ordners.
Der folgende Befehl wird beispielsweise eine Datei erstellt die Netzwerkkonfigurationsdaten über den Container enthält.

''' PowerShell
Ipconfig > c:\ipconfig.txt


```

You can read the contents of the file to ensure the command completed successfully. Notice that the IP address contained in the text file matches that of the container.

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-E0D87408-325B-4818-ADB2-2EC7A2005739-0):

   Connection-specific DNS Suffix  . : corp.microsoft.com
   Link-local IPv6 Address . . . . . : fe80::400e:1e0e:591c:beef%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1

```

Nun, dass der Container geändert wurde, beenden Sie die PowerShell-Remotesitzung.

''' PowerShell
exit


```

Stop the container by providing the container name to the `Stop-Container` command. When this command has completed, you will be back in control of the container host.

``` PowerShell
Stop-Container -Name "MyContainer"

```


###Schritt 2: Erstellen Sie ein neues Container-Bild

Ein Bild kann nun von diesem Container vorgenommen werden.
Dieses Bild kann verhält sich wie eine Momentaufnahme des Containers und erneut bereitgestellt, oft.

Erstellen Sie ein neues Bild mit dem Namen "Newimage" Verwenden der `New-ContainerImage` -Befehl abgerufen wird.
Beim Verwenden dieses Befehls geben Sie den Container zu erfassen, einen Namen für das neue Abbild und zusätzliche Metadaten gesehen unten.

''' PowerShell
$newimage = New ContainerImage - ContainerName MyContainer-Verleger Demo - Name Newimage-Version 1.0


```

Use `Get-ContainerImage` to return a list of Container Images. Notice that a new image with the name 'newimage' has been created.

``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
newimage          CN=Demo      1.0.0.0      False
WindowsServerCore CN=Microsoft 10.0.10254.0 True

```


###Schritt 3: Erstellen von neuen Container aus Bild

Nun, dass Sie eine benutzerdefinierte Container-Abbild erstellt haben, fahren Sie fort, und Bereitstellen Sie einen neuen Container dieses Abbild.

Erstellen Sie einen Container mit dem Namen "Newcontainer" aus dem Container-Abbild mit dem Namen "Newimage", und geben Sie das Ergebnis einer Variablen namens "$newcontainer".

''' PowerShell
$newcontainer = New-Container-Namen "Newcontainer" - ContainerImageName Newimage - SwitchName "Virtueller Switch"


```

Start the new container.
``` PowerShell
Start-Container $newcontainer

```

Erstellen Sie eine remote-PowerShell-Sitzung mit dem Container.
''' PowerShell
Geben Sie-PSSession - des Elements, $newcontainer. -RunAsAdministrator des Elements


```

Finally notice that this new container contains the ipconfig.txt file created earlier in this exercise.

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-E0D87408-325B-4818-ADB2-2EC7A2005739-0):

   Connection-specific DNS Suffix  . : corp.microsoft.com
   Link-local IPv6 Address . . . . . : fe80::400e:1e0e:591c:beef%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1

```

 Sobald Sie fertig sind arbeiten mit diesem Container, die PowerShell-Remotesitzung zu beenden.

''' PowerShell
exit


```

This exercise has shown that an image taken from a modified container will include all modifications. While the example here was a simple file modification, the same would apply if you were to install software into the container such as a web server. Using these methods, custom images can be created that will deploy application ready containers.

### Step 4 - Remove Containers and Container Images

To stop all running containers run the command below. If any containers are in a stopped state when you run this command, you receive a warning, which is ok.

``` PowerShell
Get-Container | Stop-Container

```

Führen Sie Folgendes ein, um alle Container zu entfernen.

''' PowerShell
Get-Container | Entfernen eines Containers-Force


```
To remove the container image named 'newimage', run the following.

``` PowerShell
Get-ContainerImage -Name newimage | Remove-ContainerImage -Force

```


##Hosten von einem Webserver in einem Container

Im folgenden Beispiel wird einen praktikabler Anwendungsfall für Windows Server-Container gezeigt.
In dieser Übung enthaltenen Schritte führt Sie durch die Erstellung einer Web-Container Serverabbild, das zum Bereitstellen von Web-Applikationen in einem Windows Server-Container verwendet werden kann.

###Schritt 1: Erstellen des Containers aus Windows Server Core-Betriebssystemabbild

Um ein Web-Server-Container-Image zu erstellen, müssen Sie zuerst bereitstellen und starten einen Container aus dem Windows Server Core-Betriebssystem-Image.
` PowerShell
$container = New-Container -Name webbase -ContainerImageName WindowsServerCore -SwitchName "Virtual Switch"
 `

Starten Sie den Container.
''' PowerShell
Start-Container $container


```

When the container is up, create a remote PowerShell session with the container.
``` PowerShell
Enter-PSSession -ContainerId $container.ContainerId -RunAsAdministrator

```


###Schritt 2 - Webserver-Software installieren

Der nächste Schritt ist die Webserver-Software zu installieren.
In diesem Beispiel wird die Nginx für Windows verwendet.
Verwenden Sie die folgenden Befehle automatisch herunterladen und extrahieren die Software Nginx c:\nginx-1.9.3.
**Hinweis** dass bei diesem Schritt den Container-Host mit dem Internet verbunden sein.
Wenn dieser Schritt führt ein Auflösung Fehler Konnektivität oder den Namen die Netzwerkkonfiguration des Hosts Container überprüfen.

Die Nginx-Software herunterladen.
''' PowerShell
Wget - Uri 'http://nginx.org/download/nginx-1.9.3.zip'-Ausgabedatei "c:\nginx-1.9.3.zip"


```

Extract the nginx software.
``` PowerShell
Expand-Archive -Path C:\nginx-1.9.3.zip -DestinationPath c:\ -Force

```

Dies ist für die Nginx-Softwareinstallation abgeschlossen werden muss.

Die remote-PowerShell-Sitzung zu beenden.
''' PowerShell
exit


```

Stop the container using the following command. 
``` PowerShell
Stop-Container $container

```


###Schritt 3: Erstellen des Abbilds aus Container für Web-Server

Mit dem Container geändert, damit die Webserver-Software Nginx enthalten können Sie jetzt ein Bild aus diesem Container erstellen.
Führen Sie dazu den folgenden Befehl aus:
''' PowerShell
$webserverimage = New ContainerImage-Container $container-Verleger Demo - Name Nginxwindows-Version 1.0


```
When completed, use the `Get-ContainerImage` command to validate that the image has been created.

``` PowerShell
Get-ContainerImage

Name              Publisher    Version      IsOSImage
----              ---------    -------      ---------
nginxwindows      CN=Demo      1.0.0.0      False
WindowsServerCore CN=Microsoft 10.0.10254.0 True

```


###Schritt 4: Bereitstellen der Container der Web-Server bereit

Verwenden Sie zum Bereitstellen einer Windows Server-Container Grundlage des Abbilds 'Nginxwindows' der `New-Container` PowerShell-Befehl.

''' PowerShell
$webservercontainer = New-Container-Namen webserver1 - ContainerImageName Nginxwindows - SwitchName "Virtueller Switch"


```

Start the container.
``` PowerShell
Start-Container $webservercontainer

```

Erstellen Sie eine remote-PowerShell-Sitzung mit den neuen Container.
''' PowerShell
Geben Sie-PSSession - des Elements, $webservercontainer. -RunAsAdministrator des Elements


```

Once working inside the container, the nginx web server can be started and web content staged. To start the nginx web server, change to the nginx installation directory.
``` PowerShell
cd c:\nginx-1.9.3\

```

Starten Sie den Nginx-Webserver.
''' PowerShell
Nginx starten


```

And exit this PS-Session.  The web server will keep running.
``` PowerShell
exit

```


###Schritt 5 - Container-Netzwerk konfigurieren

Abhängig von der Konfiguration des Containers Host- und Netzwerk erhalten ein Container entweder eine IP-Adresse von einem DHCP-Server oder den Container Host selbst mit Netzwerkadressübersetzung (NAT).
Diese Anleitung erörtert wird so konfiguriert, dass NAT verwenden.
In dieser Konfiguration wird ein Port aus dem Container einen Port auf dem Host Container zugeordnet.
Die in den Container gehostete Anwendung erfolgt dann über die IP-Adresse / Name des Container-Hosts.
Zum Beispiel wenn Port 80 aus dem Container Port 55534 auf dem Host Container zugeordnet wurde, eine Standard-http-Anforderung an die Anwendung sieht dieser Http://contianerhost:55534.
Dadurch wird einen Container Host viele Container ausführen und die Anwendung in diesen Containern zur Beantwortung von Abfragen, die den gleichen Port verwenden.

Für diese Übungseinheit müssen wir diese Zuordnung zu erstellen.
Dazu müssen wir wissen, die IP-Adresse des Containers sowie interne (Anwendung) und extern (Container-Host)-Ports, die konfiguriert werden.
Lassen Sie für dieses Beispiel uns einfach zu halten und Zuordnen von Port 80 aus dem Container an Port 80 des Hosts.
Wenn der Wert `Add-NetNatStaticMapping` Befehl, der `–InternalIPAddress` werden die IP-Adresse des Containers die in dieser exemplarischen Vorgehensweise '172.16.0.2' ausgeführt werden.

''' PowerShell
"ContainerNat" hinzufügen NetNatStaticMapping - NatName-TCP - ExternalIPAddress 0.0.0.0 - InternalIPAddress 172.16.0.2 - InternalPort 80 - ExternalPort 80-Protokolls


```
When the port mapping has been created you will also need to configure an inbound firewall rule for the configured port. To do so for port 80 run the following command. This script can be copied into the VM. 

``` PowerShell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}

```

Wenn Sie von Azure arbeiten und nicht bereits einen Endpunkt des virtuellen Computers erstellt haben müssen Sie als Nächstes jetzt eine erstellen.
Weitere Informationen zum Azure-VM-Endpunkten finden Sie in diesem Artikel: [Einrichten von Azure-VM-Endpunkten](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/).

###Schritt 6: Zugriff auf die Container-gehosteten Website

Mit dem Webcontainer erstellt haben können Sie jetzt zur Kasse gehen die in den Container gehostete Anwendung.
Hierzu öffnen Sie einen Browser auf anderen Computer aus, und geben Sie `http://containerhost-ipaddress`.
Beachten Sie, dass Sie die IP-Adresse von Host-Container und der Container selbst nicht durchsuchen.
Bei Verwendung von virtuellen Azure-Computer werden die öffentlichen IP-Adresse oder Cloud-Dienst.

Wenn alles richtig konfiguriert wurde, sehen Sie die Nginx-Willkommensseite.

!(media/nginx.png)

An diesem Punkt können Sie die Website zu aktualisieren.
In Ihrer eigenen Beispielwebsite kopieren Sie, oder verwenden Sie eine einfache "Hello World"-Beispielsite, die erstellt wurde, für diese Demo.
Verwenden des Beispiels Sie zunächst eine remote-PS-Sitzung mit dem Container neu einrichten müssen.

Sie müssen zunächst die PS-Remotesitzung mit dem Container neu zu erstellen.
''' PowerShell
Geben Sie-PSSession - des Elements, $webservercontainer. -RunAsAdministrator des Elements


```
Then run the following command to download and replace the index.html file.

``` powershell
wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx-1.9.3\html\index.html"

```

Nachdem die Website aktualisiert wurde, navigieren Sie zurück zu `http://containerhost-ipaddress`.

!(media/hello.png)

##Video zur exemplarischen Vorgehensweise

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-PowerShell/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="a766cb39-e567-43ed-a0f4-a67855392438" />

##Nächste Schritte

Nun die Container einrichten sowie eine Einführung in die Tools, fahren Sie Ihren eigenen Sammelartikeleinheit apps zu erstellen.

Hier ist eine vollständigere [PowerShell-Referenz](../reference/powershell_overview.md).

Beachten Sie, dass dies ist ein **Vorschau** Es sind Fehler aufgetreten sind, und wir haben viel Arbeit.
[Auf dieser Seite](../about/work_in_progress.md) enthält viele unserer bekannter Probleme.

Wir sind auch: Überwachen der [-Foren](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers) sehr genau.

Dazu gehören auch vorgefertigte Beispiele auf [GitHub](https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples).

-----------------------------------
[Back to Container Home](../containers_welcome.md)   
[Known Issues for Current Release](../about/work_in_progress.md)


