MS. ContentId: 1ab7bfe1-da35-4ff1-916f-936fedf536a0
Titel: Einrichten von Windows-Container in Azure

#Vorbereiten von Microsoft Azure für Windows Server-Container

Vor dem Erstellen und Verwalten von Windows Server-Containern in Azure müssen Sie ein Abbild von Windows Server 2016: Technische Vorschau bereitstellen, die mit der Funktion Servercontainer Windows vorkonfiguriert wurde.
Diese Anleitung führt Sie durch diesen Vorgang.

> Handbücher mit anderen ersten Schritten:
> 

*   Führen Sie im Windows Server-Container [ein neuer virtueller Computer für Hyper-V](./container_setup.md).
*   Führen Sie im Windows Server-Container [vorhandenen virtuellen Computer](./inplace_setup.md)
*   Einrichten von Windows Server-Container [auf einer physischen Windows Server Core-installation](./inplace_setup.md)

##Starten Sie mithilfe von Azure-Portal

Wenn Sie ein Azure-Konto haben, fahren Sie direkt mit [Erstellen Sie einen Container-Host-VM](#CreateacontainerhostVM).

1.  Gehe zu [Azure.com](https://azure.com) und die Schritte für eine [Kostenlose Azure-Testversion](https://azure.microsoft.com/en-us/pricing/free-trial/).
2.  Melden Sie sich mit Ihrem Microsoft-Konto.
3.  Wenn Ihr Konto einsatzbereit ist, melden Sie sich bei der [Azure-Verwaltungsportal](https://portal.azure.com).

##Erstellen Sie einen Container-Host-VM

Klicken Sie auf den folgenden Link, um den Erstellungsprozess für den virtuellen Computer zu starten: [Neue Windows Server-Container-Host in Azure](https://portal.azure.com/#gallery/Microsoft.WindowsServer2016TechnicalPreviewwithContainers).

Sie können auch für das Image im Azure-Katalog suchen.

Klicken Sie auf der `create` Schaltfläche.

!(./media/newazure1.png)

Geben Sie den virtuellen Computer einen Namen ein, wählen Sie einen Benutzernamen und ein Kennwort.

!(media/newazure2.png)

Wählen Sie die optionale Konfiguration > Endpunkte >, und geben Sie einen HTTP-Endpunkt mit einem privaten und öffentlichen Port 80, wie unten dargestellt.
Wenn Fertig klicken Sie auf "ok" zweimal.

!(./media/newazure3.png)

Aktivieren Sie die Option `create` Schaltfläche, um den Bereitstellungsprozess für die virtuellen Computer zu starten.

!(media/newazure2.png)

Wenn die VM-Bereitstellung abgeschlossen ist, wählen Sie die Schaltfläche "Verbinden", um eine RDP-Sitzung mit dem Windows Server-Host-Container zu starten.

!(media/newazure6.png)

Melden Sie sich auf dem virtuellen Computer mit dem Benutzernamen und Kennwort angegeben werden, während der Assistent zum Erstellen von VM.
Nach der Anmeldung in Suchen Sie in einer Windows-Befehlszeile.

!(media/newazure7.png)

##Video zur exemplarischen Vorgehensweise

<iframe src="https://channel9.msdn.com/Blogs/containers/Quick-Start-Configure-Windows-Server-Containers-in-Microsoft-Azure/player" width="800" height="450" allowFullScreen="true" frameBorder="0" scrolling="no" caps_internal_Id="f5f02a2b-813f-439f-a3ce-dcf1a3768b2a" />

##Nächste Schritte – starten Sie mithilfe von Containern

Jetzt, eine Windows Server-2016 durch Ausführen der Funktion Servercontainer Windows System zur Arbeit mit Windows Server-Containern und Windows Server-Container Bilder die folgenden Handbücher zu wechseln.

[Schnellstart: Windows Server-Container und Docker](./manage_docker.md)[Schnellstart: Windows Server-Container und PowerShell](./manage_powershell.md)

-------------------
[Back to Container Home](../containers_welcome.md)  
[Known Issues for Current Release](../about/work_in_progress.md)


