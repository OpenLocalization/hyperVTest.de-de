MS. ContentId: 71a03c62-50fd-48dc-9296-4d285027a96a
Titel: Windows-Container auf einem lokalen virtuellen Computer einrichten

#Vorbereiten der Technologievorschau der Windows Server für Windows Server-Container

Zum Erstellen und Verwalten von Windows Server-Container, muss die Technologievorschau der Windows Server 2016 Umgebung vorbereitet werden.
Dieses Handbuch führt durch die Konfiguration von Windows Server-Container auf einem virtuellen Hyper-V-Computer.

> Handbücher mit anderen ersten Schritten:
> 

*   Führen Sie im Windows Server-Container [Azure](./azure_setup.md).
*   Führen Sie im Windows Server-Container [vorhandenen virtuellen Computer](./inplace_setup.md).
*   Einrichten von Windows Server-Container [auf einer physischen Windows Server Core-installation](./inplace_setup.md).
    
    **LESEN SIE VOR DER INSTALLATION DES CONTAINER-BS-IMAGE:**  Dem Lizenzvertrag von Microsoft Windows Server-Vorabversion der Software ("Lizenzbedingungen"), gelten für die Verwendung des Microsoft Windows-Container-Betriebssystemabbild Zusatzes ("zusätzliche Software).
    Durch Herunterladen und verwenden die Zusatzsoftware, stimmen Sie dem Lizenzvertrag und können Sie nicht verwenden, wenn Sie dem Lizenzvertrag nicht akzeptiert haben.
    Windows Server-Vorabversion der Software und die Zusatzsoftware werden von der Microsoft Corporation lizenziert.
    
    *   System unter Windows 10 / Windows Server Technical Preview 2 oder höher.
    *   Hyper-V-Rolle aktiviert)[Anweisungen finden Sie](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install#UsingPowerShell)).
    *   20GB freier Speicherplatz für Container Host Image, Base Betriebssystemabbild und Setup-Skripts.
    *   Administratorberechtigungen auf dem Hyper-V-Host.

> Windows Server-Container erfordern keine Hyper-V, aber der Einfachheit halber dieses Handbuch setzt voraus, dass eine Hyper-V-Umgebung verwendet wird, um den Container für Windows Server-Host ausgeführt werden.
> 

##Einen neuen Container-Host auf einen neuen virtuellen Computer einrichten

Windows Server-Container bestehen aus mehreren Komponenten, z. B. die Windows Server-Container-Host und die Basis-Betriebssystemabbild Container.
Wir haben ein Skript zusammengestellt, die herunterladen und konfigurieren diese Elemente für Sie.
Führen Sie diese Schritte, um einen neuen Hyper-V virtuelle Computer bereitstellen und Konfigurieren dieses System als Windows Server-Host-Container.

Starten einer PowerShell-Sitzungs als Administrator an.
Dies kann durch Rechtsklick auf das Symbol "PowerShell" und Auswählen von "Ausführen als Administrator" oder durch Ausführen des folgenden Befehls aus einer PowerShell-Sitzung erfolgen.

''' Powershell
Start-Process-Powershell-Verb "runas"


```

Use the following command to download the configuration script. The script can also be manually downloaded from this location - [Configuration Script](http://aka.ms/newcontainerhost).

``` PowerShell
wget -uri https://aka.ms/newcontainerhost -OutFile New-ContainerHost.ps1

```

Führen Sie den folgenden Befehl zum Erstellen und konfigurieren Sie die Container, in dem `<containerhost>` Der Name des virtuellen Computers und `<password>` das Kennwort wird des Administratorkontos zugewiesen werden.

''' Powershell
.\New-ContainerHost.ps1 – VmName < Containerhost >-< Kennwort >


```

When the script begins you will be asked to read and accept licensing terms.


```

Vor der Installation und Verwendung von Windows Server Technical Preview 3 mit Containern virtuellen Computer müssen Sie folgende Aktionen ausführen:
    1
Überprüfen Sie den Lizenzvertrag durch wechseln zu diesem Link: http://aka.ms/WindowsServerTP3ContainerVHDEula
    2.
Drucken Sie die Lizenzbedingungen aus, und heben Sie eine Kopie für Ihre Unterlagen auf.
Durch Herunterladen und Verwenden von Windows Server Technical Preview 3 mit Containern virtuellen Computer stimmen Sie z. B.
Lizenzvertrag.
Bitte bestätigen Sie akzeptiert haben und dem Lizenzvertrag zustimmen.
[N] keine [J] Ja [?] Hilfe (Standardeinstellung ist "N"): „Y“ zugeordnet ist


```

The script will then begin to download and configure the Windows Server Container components. This process may take quite some time due to the large download. When finished your Virtual Machine will be configured and ready for you to create and manage Windows Server Containers and Windows Server Container Images with both PowerShell and Docker.  

You may receive the following message during the Window Server Container host deployment process. 

```

Dieser virtuelle Computer ist nicht mit dem Netzwerk verbunden. Um es zu verbinden, führen Sie Folgendes ein:
Get-VM | Get-VMNetworkAdapter | Verbinden-VMNetworkAdapter - Switchname < Switchname >


```
If you do, check the properties of the virtual machine and connect the virtual machine to a virtual switch. You can also run the following PowerShell command where `<switchname>` is the name of the Hyper-V virtual switch that you would like to connect to the virtual machine.

``` powershell 
Get-VM | Get-VMNetworkAdapter | Connect-VMNetworkAdapter -Switchname <switchname>

```

Wenn das Skript abgeschlossen ist, starten Sie den virtuellen Computer.
Der virtuelle Computer mit Windows Server 2016 Core konfiguriert ist und sieht wie folgt aus.

< Center >!(./media/containerhost2.png)< / center >< Br / >

Schließlich melden Sie sich mit das Kennwort angegeben werden, bei der Konfiguration des virtuellen Computers, und stellen Sie sicher, dass die virtuelle Maschine über eine gültige IP-Adresse verfügt.
Mit diesen Elementen abgeschlossen sollte Ihr System für die Windows Server-Container bereit.

##Video zur exemplarischen Vorgehensweise

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Configure-Windows-Server-Containers-on-a-Local-System/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="41310593-862b-46c4-8965-53ffe730ae48" />

##Nächste Schritte – starten Sie mithilfe von Containern

Jetzt, eine Windows Server-2016 durch Ausführen der Funktion Servercontainer Windows System zur Arbeit mit Windows Server-Containern und Windows Server-Container Bilder die folgenden Handbücher zu wechseln.

[Schnellstart: Windows Server-Container und Docker](./manage_docker.md)

[Schnellstart: Windows Server-Container und PowerShell](./manage_powershell.md)

-------------------

[Zurück zur Startseite von Container](../containers_welcome.md)[Bekannte Probleme bei der aktuellen Version](../about/work_in_progress.md)


