MS. ContentId: 347fa279-d588-4094-90ec-8c2fc241f5b6
Titel: Verwalten von Windows Server-Container mit Docker

#Schnellstart: Windows Server-Container und Docker

In diesem Artikel werden die Grundlagen der Verwaltung von Windows Server-Container mit Docker durchlaufen.
Container für Windows Server und Windows Server-Container-Images erstellen, entfernen Windows Server-Container und Container Bilder und Bereitstellen einer Anwendung in einem Windows Server-Container, werden die behandelten Elemente umfassen.
Die gewonnenen Erkenntnisse in dieser exemplarischen Vorgehensweise sollten Sie zu untersuchen, Bereitstellung und Verwaltung von Windows Server-Container mit Docker aktivieren.

Haben Sie Fragen?
Bitten Sie sie auf der [Windows-Container-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers).

> **Hinweis:** Mit PowerShell erstellten Windows-Container können nicht mit Docker und umgekehrt derzeit verwaltet werden.
> Container mit PowerShell erstellen, finden Sie unter  [Schnellstart: Windows Server-Container und PowerShell](./manage_powershell.md).
> < Br / >< Br / > Wenn Sie mehr wissen möchten, [Häufig gestellte Fragen](../about/faq.md#WhydoIhavetopickbetweenDockerandPowerShellforWindowsServerContainermanagement).
> 

##Voraussetzungen

Zum Durchführen dieser exemplarischen Vorgehensweise müssen die folgenden Elemente vorhanden sein.

*   Windows Server 2016 TP3 oder später mit dem Container-Feature von Windows Server konfiguriert.
    Wenn Sie das Handbuch abgeschlossen haben, ist dies die VM, die in Azure oder Hyper-V erstellt wurde.
*   Dieses System muss mit einem Netzwerk verbunden und auf das Internet zugreifen kann.

Wenn Sie die Container-Funktion konfigurieren müssen, finden Sie in den folgenden Handbüchern: [Container-Einrichtung in Azure](./azure_setup.md) oder [Container-Setup in Hyper-V](./container_setup.md).

##Grundlegender Container-Verwaltung mit Docker

In diesem ersten Beispiel werden die Grundlagen zum Erstellen und Entfernen von Containern für Windows Server und Windows Server-Container-Images mit Docker geführt.

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


> Dieser Schnellstart konzentriert werden, jedoch einige Schritte ausführen, wie z. B. Verwalten von Firewallregeln und Kopieren von Dateien mit PowerShell-Befehlen ausgeführt werden, auf Docker-Befehle.
> Durcharbeiten dieser exemplarischen Vorgehensweise aus einer PowerShell-Sitzung.
> 

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

Vor dem Erstellen einer Windows Server-Container mit Docker benötigen Sie den Namen oder die ID eines Exsisitng Container für Windows Server-Abbilds.

Um alle Bilder geladen werden, auf dem Host Container verwenden, finden Sie unter der `docker images` -Befehl abgerufen wird.

''' PowerShell
Docker Bilder

REPOSITORY-TAG-ID ERSTELLT VIRTUELLE BILDGRÖSSE
Windowsservercore neueste 9eca9231f4d4 30 Stunden 9.613 GB
Windowsservercore 10.0.10254.0 9eca9231f4d4 30 Stunden 9.613 GB


```

Now, use `docker run` To create a new Windows Server Container. This command as seen below will instruct the Docker daemon to create a new container named ‘dockerdemo’ from the image ‘windowsservercore’ and open an interactive (-it) console session (cmd) with the container.

``` PowerShell
docker run -it --name dockerdemo windowsservercore cmd

```

Nach Abschluss des Befehls werden Sie in einer Konsolen-Sitzung für den Container arbeiten.

Arbeiten in einem Container ist fast identisch mit der Arbeit mit Windows auf einem virtuellen oder physischen Computer installiert.
Sie können z. B. Befehle ausführen `ipconfig` die IP-Adresse des Containers zurückgeben `mkdir` Erstellen Sie ein neues Verzeichnis, oder `powershell` Um eine PowerShell-Sitzung zu starten.
Fahren Sie fort, und nehmen Sie eine Änderung an dem Container, z. B. das Erstellen einer Datei oder eines Ordners.
Der folgende Befehl wird beispielsweise eine Datei erstellt die Netzwerkkonfigurationsdaten über den Container enthält.

''' PowerShell
Ipconfig > c:\ipconfig.txt


```

You can read the contents of the file to ensure the command completed successfully. Notice that the IP address contained in the text file matches that of the container.

``` PowerShell
type c:\ipconfig.txt

Ethernet adapter vEthernet (Virtual Switch-94a3e12ad262b3059e08edc4d48fca3c8390e38c3b219023d4a0a4951883e658-0):

   Connection-specific DNS Suffix  . : 
   Link-local IPv6 Address . . . . . : fe80::cc1f:742:4126:9530%18
   IPv4 Address. . . . . . . . . . . : 172.16.0.2
   Subnet Mask . . . . . . . . . . . : 255.240.0.0
   Default Gateway . . . . . . . . . : 172.16.0.1

```

Jetzt, dass der Container geändert wurde, führen Sie Folgendes ein, um das Beenden der Konsole Sitzung platzieren Sie in der Konsole-Sitzung des Hosts Container zurück.

''' PowerShell
exit


```

Finally to see a list of containers on the container host use the `docker ps –a` command. Notice from the output that a container named 'dockerdemo' has been created.

``` PowerShell
docker ps -a

CONTAINER ID        IMAGE               COMMAND        CREATED             STATUS                     PORTS     NAMES
4f496dbb8048        windowsservercore   "cmd"          2 minutes ago       Exited (0) 2 minutes ago             dockerdemo

```


###Schritt 2: Erstellen Sie ein neues Container-Bild

Ein Bild kann nun von diesem Container vorgenommen werden.
Dieses Bild kann verhält sich wie eine Momentaufnahme des Containers und erneut bereitgestellt, oft.

Erstellen Sie ein neues Abbild führen Sie die folgenden.
Dieser Befehl weist das Modul Docker, erstellen Sie ein neues Bild mit dem Namen "Newcontainerimage", die alle Änderungen an den Container "Deckerdemo" enthalten sein sollen.

''' PowerShell
Docker Commit Dockerdemo newcontainerimage


```

To see all images on the host, run `docker images`. Notice that a new image has been created with the name 'newcontainerimage'.

``` PowerShell
docker images

REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
newcontainerimage   latest              4f8ebcf0a334        2 minutes ago       9.613 GB
windowsservercore   latest              9eca9231f4d4        30 hours ago        9.613 GB
windowsservercore   10.0.10254.0        9eca9231f4d4        30 hours ago        9.613 GB

```


###Schritt 3: Erstellen von neuen Container aus Bild

Nun, da Sie ein benutzerdefinierter Container Bild haben, Bereitstellen Sie einen neuen Container mit dem Namen 'Newcontainer' von 'Newcontainerimage', und öffnen Sie eine interaktive Shell-Sitzung mit dem Container.

''' PowerShell
Docker ausgeführt – es veröffentlicht – Name Newcontainer Newcontainerimage Cmd


```

Take a look at the c:\ drive of this new container and notice that the ipconfig.txt file is present.

![](media/docker3.png)

Exit the newly created container to return to the container hosts console session.

``` PowerShell
exit

```

In dieser Übung ergab, dass ein Abbild stammt aus einer geänderten Container alle Änderungen enthalten sein sollen.
Im Beispiel wird eine einfache Änderung war, zwar gilt die gleiche würden Sie Software in den Container, z. B. einen Webserver zu installieren.
Mithilfe dieser Methoden können benutzerdefinierte Abbilder erstellen, die Anwendung bereit Containern bereitgestellt werden soll.

###Schritt 4: Entfernen von Containern und Bilder

Um einen Container zu entfernen, wenn es nicht mehr benötigt verwenden die `docker rm` -Befehl abgerufen wird.
Der folgende Befehl entfernt den Container "Newcontainer".

''' PowerShell
Docker Rm newcontainer


```
To remove container images when they are no longer needed use the `docker rmi` command. You cannot remove an image if it is referenced by an existing container.

The following command removes the container image named 'newcontainerimage'.
``` PowerShell
docker rmi newcontainerimage

Untagged: newcontainerimage:latest
Deleted: 4f8ebcf0a334601e75070a92294d993b0f182abb6f4c88740c75b05093e6acff

```


##Hosten von einem Webserver in einem Container

Im folgenden Beispiel wird einen praktikabler Anwendungsfall für Windows Server-Container gezeigt.
In dieser Übung enthaltenen Schritte führt Sie durch die Erstellung einer Web-Container Serverabbild, das zum Bereitstellen von Web-Applikationen in einem Windows Server-Container verwendet werden kann.

###Schritt 1 - Webserver-Software herunterladen

Server-Software müssen vor dem Erstellen eines Abbilds Container im Web heruntergeladen und auf dem Host Container bereitgestellt werden.
Wir werden die Nginx für Windows-Software in diesem Beispiel verwenden.
**Hinweis** dass bei diesem Schritt den Container-Host mit dem Internet verbunden sein.
Wenn dieser Schritt führt ein Auflösung Fehler Konnektivität oder den Namen die Netzwerkkonfiguration des Hosts Container überprüfen.

Führen Sie den folgenden Befehl auf dem Host Container zum Erstellen der Verzeichnisstruktur, die für dieses Beispiel verwendet werden.

''' PowerShell
Mkdir c:\build\nginx\source


```

Run this command on the container host to download the nginx software to 'c:\nginx-1.9.3.zip'.

``` PowerShell
wget -uri 'http://nginx.org/download/nginx-1.9.3.zip' -OutFile "c:\nginx-1.9.3.zip"

```

Schließlich wird der folgende Befehl die Nginx-Software für die 'C:\build\nginx\source' extrahiert.

''' PowerShell
Erweitern Sie Archiv-Pfad C:\nginx-1.9.3.zip DestinationPath - C:\build\nginx\source-Force


```

### Step 2 - Create Web Server Image
In the previous example, you manually created, updated and captured a container image. This example will demonstrate an automated method for creating container images using a Dockerfile. Dockerfiles contain instructions that the Docker engine uses to build and modify a container, and then commit the container to a container image. 
For more information on dockerfiles, see [Dockerfile reference](https://docs.docker.com/reference/builder/).

Use the following command to create an empty dockerfile.

``` PowerShell
new-item -Type File c:\build\nginx\dockerfile

```

Öffnen Sie die Dockerfile mit Notepad.


```
notepad.exe c:\build\nginx\dockerfile

```

Kopieren Sie den folgenden Text in Editor, speichern Sie die Datei, und schließen Sie Editor.

''' PowerShell
AUS windowsservercore
Bezeichnung Description = "Nginx für Windows" Vendor = "Nginx" Version = "1.9.3"
Hinzufügen von Datenquellen /nginx


```

At this point the dockerfile will be in 'c:\build\nginx' and the nginx software extracted to 'c:\build\nginx\source'. 
You are now ready to build the web server container image based on the instructions in the dockerfile. To do this, run the following command on the container host.

``` PowerShell
docker build -t nginx_windows C:\build\nginx

```

Dieser Befehl weist das Docker-Modul verwenden, die am dockerfile `C:\build\nginx` So erstellen Sie ein Abbild mit dem Namen "Nginx_windows".

Die Ausgabe sieht etwa wie folgt:

!(media/docker1.png)

Wenn abgeschlossen ist, sehen Sie sich die Bilder auf dem Host mit der `docker images` -Befehl abgerufen wird.
Ein neues Bild mit dem Namen "Nginx_windows" sollte angezeigt werden.
''' PowerShell
Docker Bilder

REPOSITORY-TAG-ID ERSTELLT VIRTUELLE BILDGRÖSSE

Nginx_windows neueste d792268338d0 vor 5 Sekunden 9.613 GB
Windowsservercore 10.0.10254.0 9eca9231f4d4 35 Stunden 9.613 GB
Windowsservercore neueste 9eca9231f4d4 35 Stunden 9.613 GB


```

### Step 3 – Configure Networking for Container Application
Because you will be hosting a website inside of a container a few networking related configurations need to be made. First a firewall rule needs to be created on the container host that will allow access to the website. In this example we will be accessing the site through port 80. Run the following script to create this firewall rule. This script can be copied into the VM. 

``` powershell
if (!(Get-NetFirewallRule | where {$_.Name -eq "TCP80"})) {
    New-NetFirewallRule -Name "TCP80" -DisplayName "HTTP on TCP/80" -Protocol tcp -LocalPort 80 -Action Allow -Enabled True
}

```

Wenn Sie von Azure arbeiten und nicht bereits einen Endpunkt des virtuellen Computers erstellt haben müssen Sie als Nächstes jetzt eine erstellen.
Weitere Informationen zum Azure-VM-Endpunkten finden Sie in diesem Artikel: [Einrichten von Azure-VM-Endpunkten](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-set-up-endpoints/).

###Schritt 4: Bereitstellen der Container der Web-Server bereit

Führen den folgenden Befehl, um einen Windows Server-Container basiert, von der 'Nginx_windows' bereitstellen Container.
Erstellt einen neuen Container mit dem Namen 'Nginxcontainer' und starten eine konsolensitzung für die für den Container.
Der – p 80:80 Teil dieser Befehl erstellt eine Port-Zuordnung zwischen Port 80 auf dem Host auf Port 80 für den Container.

''' Powershell
run - Docker es veröffentlicht – Name Nginxcontainer -p 80:80 Nginx_windows Cmd


```
Once working inside the container, the nginx web server can be started and web content staged. To start the nginx web server, change to the nginx installation directory.

``` powershell
cd c:\nginx\nginx-1.9.3

```

Starten Sie den Nginx-Webserver.
''' Powershell
Nginx starten


```
### Step 5 – Access the Container Hosted Website

With the web server container created, you can now checkout the application hosted in the container. To do so, open up a browser on different machine and enter `http://containerhost-ipaddress`. Notice here that you will be browsing to the IP Address of the Container Host and not the container itself. If you are working from an Azure Virtual Machine this will be the public IP address or Cloud Service name. 

If everything has been correctly configured, you will see the nginx welcome page.

![](media/nginx.png)

At this point, feel free to update the website. Copy in your own sample website, or run the following command in the container to replace the nginx welcome page with a ‘Hello World’ web page.

```powershell
powershell wget -uri 'https://raw.githubusercontent.com/Microsoft/Virtualization-Documentation/master/doc-site/virtualization/windowscontainers/quick_start/SampleFiles/index.html' -OutFile "C:\nginx\nginx-1.9.3\html\index.html"

```

Nachdem die Website aktualisiert wurde, navigieren Sie zurück zu `http://containerhost-ipaddress`.

!(media/hello.png)

> **Hinweis:** Wenn die Docker-Daemon-Einstellungen (z. B. den Port zu ändern, es überwacht, Remoteverbindung zu einem Container) ändern möchten, müssen Sie zum Bearbeiten der Datei "C:\ProgramData\docker\runDockerDaemon.cmd" im Container und müssen Sie den Dienst mit PowerShell neu starten, `Restart-Service docker`.
> 

##Video zur exemplarischen Vorgehensweise

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Deploying-and-Managing-Windows-Server-Containers-with-Docker/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="d1e56d51-7235-4f44-873b-06f6bfc59ed7" />

##Nächste Schritte

Nun die Container einrichten sowie eine Einführung in die Tools, fahren Sie Ihren eigenen Sammelartikeleinheit apps zu erstellen.

Beachten Sie, dass dies ist ein **Vorschau** Es sind Fehler aufgetreten sind, und wir haben viel Arbeit.
[Auf dieser Seite](../about/work_in_progress.md) enthält viele unserer bekannter Probleme.

Beachten Sie, dass es gibt einige bekannte Docker-Befehle [funktionieren nicht](../about/work_in_progress.md#DockermanagementDockercommandsthatdontworkwithWindowsServerContainers) und dass nur einige [teilweise funktionsfähig](../about/work_in_progress.md#DockermanagementDockercommandsthatpartiallyworkwithWindowsServerContainers)

Wir sind auch: Überwachen der [-Foren](https://social.msdn.microsoft.com/Forums/en-US/home?forum=windowscontainers) sehr genau.

Dazu gehören auch vorgefertigte Beispiele auf [GitHub](https://github.com/Microsoft/Virtualization-Documentation/tree/master/windows-server-container-samples).

-----------------------------------
[Back to Container Home](../containers_welcome.md)   
[Known Issues for Current Release](../about/work_in_progress.md)


