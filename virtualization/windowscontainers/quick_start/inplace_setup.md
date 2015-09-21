MS. ContentId: 44b138bb-962f-4474-a0c4-284646a872e2
Titel: Einrichten von Windows-Containern vorhanden

#Vorbereiten von einem physischen Computer oder einem vorhandenen virtuellen Computer für Windows Server-Container

Zum Erstellen und Verwalten von Windows Server-Container, muss die Technologievorschau der Windows Server 2016 Umgebung vorbereitet werden.
Dieses Handbuch führt durch die Konfiguration von Windows Server-Container auf bare-Metal- oder in einem vorhandenen virtuellen Computer unter Windows Server 2016 Technical Preview.

> Handbücher mit anderen ersten Schritten:
> 

*   Führen Sie im Windows Server-Container [Azure](./azure_setup.md).
*   Führen Sie im Windows Server-Container [eine neue Hyper-V-VM](./container_setup.md).
    
    **LESEN SIE VOR DER INSTALLATION DES CONTAINER-BS-IMAGE:**  Dem Lizenzvertrag von Microsoft Windows Server-Vorabversion der Software ("Lizenzbedingungen"), gelten für die Verwendung des Microsoft Windows-Container-Betriebssystemabbild Zusatzes ("zusätzliche Software).
    Durch Herunterladen und verwenden die Zusatzsoftware, stimmen Sie dem Lizenzvertrag und können Sie nicht verwenden, wenn Sie dem Lizenzvertrag nicht akzeptiert haben.
    Windows Server-Vorabversion der Software und die Zusatzsoftware werden von der Microsoft Corporation lizenziert.

**Anforderungen für System (oder virtuelle Computer):**

*   Unter Windows Server Technical Preview 3 Server Core-System.
*   10GB Speicherplatz für OS-Basis-Image und die Setup-Skripts.
*   Administratorberechtigungen auf dem Computer oder den virtuellen Computer.

##Setup einen vorhandenen virtuellen Maschine oder Bare-Metal-Host für Container

Windows Server-Container erfordern das Container-Betriebssystemabbild Base.
Wir haben ein Skript zusammengestellt, die heruntergeladen und installiert diese für Sie.
Führen Sie diese Schritte, um die Konfiguration Ihres Systems als Host für Windows Server-Container.

Starten einer PowerShell-Sitzungs als Administrator an.
Dies kann erfolgen, indem Sie den folgenden Befehl von der Befehlszeile aus ausführen.

''' Powershell
PowerShell.exe


```

Make sure the title of the windows is "Administrator: Windows PowerShell". If it does not say Administrator, run this command to run with admin priveledges:

``` powershell
start-process powershell -Verb runas

```

Verwenden Sie den folgenden Befehl aus, um das Setup-Skript herunterzuladen.
Das Skript kann auch manuell von diesem Speicherort heruntergeladen werden- [Skript für Konfiguration](http://aka.ms/setupcontainers).

''' PowerShell
die Uri - https://aka.ms/setupcontainers Wget-Ausgabedatei C:\ContainerSetup.ps1


```

 After the download completes, execute the script.
``` PowerShell
C:\ContainerSetup.ps1

```

Das Skript beginnt dann herunterladen und konfigurieren die Komponenten der Windows Server-Container.
Dieser Vorgang kann einige Zeit aufgrund der großen Download dauern.
Der Computer kann während des Vorgangs neu gestartet.
Wenn Sie fertig ist, wird der Computer konfiguriert werden und für Sie erstellen und Verwalten von Windows Server-Container und Windows Server-Container-Images mit PowerShell und Docker.

Mit diesen Elementen abgeschlossen sollte Ihr System für die Windows Server-Container bereit.

##Nächste Schritte – starten Sie mithilfe von Containern

Nun, dass Sie Windows Server-Container ausgeführt werden, wechseln Sie zu den folgenden Handbüchern zum Arbeiten mit Bildern von Containern für Windows Server und Windows Server-Container.

[Schnellstart: Windows Server-Container und Docker](./manage_docker.md)

[Schnellstart: Windows Server-Container und PowerShell](./manage_powershell.md)

-------------------

[Zurück zur Startseite von Container](../containers_welcome.md)[Bekannte Probleme bei der aktuellen Version](../about/work_in_progress.md)


