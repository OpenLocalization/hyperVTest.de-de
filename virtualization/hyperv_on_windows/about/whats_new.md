MS. ContentId: 52DAFFBE-40F5-46D2-96F3-FB8659581594 
Titel: Neues in Hyper-V für Windows 10

#Was ist neu in Hyper-V auf Windows 10

Dieses Thema erläutert die neue und geänderte Funktionen in Hyper-V auf 10 für Windows ®.

##Windows PowerShell Direct

Es ist nun eine einfache und zuverlässige Möglichkeit zum Ausführen von Windows PowerShell-Befehle in einem virtuellen Computer aus dem Hostbetriebssystem.
Es gibt keine Netzwerk- oder Firewall-Anforderungen oder eine spezielle Konfiguration.
Dies funktioniert unabhängig von der Konfiguration der remote-Verwaltung.
Verwenden möchten, müssen Sie Windows 10 oder Technical Preview für Windows Server, auf dem Host und das Gastbetriebssystem des virtuellen Computers ausführen.

Verwenden Sie zum Erstellen einer PowerShell-Direct-Sitzungs einen der folgenden Befehle aus:

''' PowerShell
Geben Sie-PSSession - VMName VMName
Invoke-Command - VMName VMName - ScriptBlock {Befehle}


```

Today, Hyper-V administrators rely on two categories of tools for connecting to a virtual machine on their Hyper-V host:
- Remote management tools such as PowerShell or Remote Desktop
- Hyper-V Virtual Machine Connection (VM Connect)

Both of these technologies work well, but each have trade-offs as your Hyper-V deployment grows. VMConnect is reliable, but it can be hard to automate. Remote PowerShell is powerful, but can be difficult to setup and maintain. 

Windows PowerShell Direct provides a powerful scripting and automation experience with the simplicity of VMConnect. Because Windows PowerShell Direct runs between the host and virtual machine, there is no need for a network connection or to enable remote management. You do need guest credentials to log into the virtual machine.

#### Requirements
- You must be connected to a Windows 10 or Windows Server Technical Preview host with virtual machines that run Windows 10 or Windows Server Technical Preview as guests.
- You need to be logged in with Hyper-V Administrator credentials on the host.
- You need User credentials for the virtual machine.
- The virtual machine you want to connect to must be running and booted.


## Hot add and remove for network adapters and memory

You can now add or remove a Network Adapter while the virtual machine is running, without downtime. This works for generation 2 virtual machines running both Windows and Linux operating systems. 

You can also adjust the amount of memory assigned to a virtual machine while it's running, even if you haven’t enabled Dynamic Memory. This works for both generation 1 and generation 2 virtual machines.

## Production checkpoints

Production checkpoints allow you to easily create “point in time” images of a virtual machine, which can be restored later on in a way that is completely supported for all production workloads. This is achieved by using backup technology inside the guest to create the checkpoint, instead of using saved state technology. For production checkpoints, the Volume Snapshot Service (VSS) is used inside Windows virtual machines. Linux virtual machines flush their file system buffers to create a file system consistent checkpoint. If you want to create checkpoints using saved state technology, you can still choose to use standard checkpoints for your virtual machine. 


> **Important:** The default for new virtual machines will be to create production checkpoints with a fallback to standard checkpoints. 


## Hyper-V Manager improvements

- **Alternate credentials support** – You can now use a different set of credentials in Hyper-V manager when you connect to another Windows 10 Technical Preview remote host. You can also save these credentials so it's easier to log on later. 

- **Down-level management** - You can now use Hyper-V manager to manage more versions of Hyper-V. With Hyper-V manager in Windows 10 Technical Preview, you can manage computers running Hyper-V on Windows Server 2012, Windows 8, Windows Server 2012 R2 and Windows 8.1.

- **Updated management protocol** - Hyper-V manager has been updated to communicate with remote Hyper-V hosts using the WS-MAN protocol, which permits CredSSP, Kerberos or NTLM authentication. When you use CredSSP to connect to a remote Hyper-V host, it allows you to perform a live migration without first enabling constrained delegation in Active Directory. WS-MAN-based infrastructure also simplifies the configuration necessary to enable a host for remote management. WS-MAN connects over port 80, which is open by default.


## Connected Standby works 

When Hyper-V is enabled on a computer that uses the Always On/Always Connected (AOAC) power model, the Connected Standby power state is now available.

In Windows 8 and 8.1, Hyper-V caused computers that used the Always On/Always Connected (AOAC) power model (also known as InstantON) to never sleep. See this [KB article](
https://support.microsoft.com/en-us/kb/2973536) for a full discription.


## Linux secure boot 

More Linux operating systems, running on generation 2 virtual machines, can now boot with the secure boot option enabled.  Ubuntu 14.04 and later, and SUSE Linux Enterprise Server 12, are enabled for secure boot on hosts that run the Technical Preview. Before you boot the virtual machine for the first time, you must specify that the virtual machine should use the Microsoft UEFI Certificate Authority.  At an elevated Windows Powershell prompt, type:

    Set-VMFirmware vmname -SecureBootTemplate MicrosoftUEFICertificateAuthority

For more information on running Linux virtual machines on Hyper-V, see [Linux and FreeBSD Virtual Machines on Hyper-V](http://technet.microsoft.com/library/dn531030.aspx).


## Virtual Machine Configuration Version 

When you move or import a virtual machine to a host running Hyper-V on Windows 10 from host running Windows 8.1, the virtual machine’s configuration file isn't automatically upgraded. This allows the virtual machine to be moved back to a host running Windows 8.1. You won't have access to new virtual machine features until you manually update the virtual machine configuration version. 

The virtual machine configuration version represents what version of Hyper-V the virtual machine’s configuration, saved state, and snapshot files it's compatible with. Virtual machines with configuration version 5 are compatible with Windows 8.1 and can run on both Windows 8.1 and Windows 10. Virtual machines with configuration version 6 are compatible with Windows 10 and won't run on Windows 8.1.

#### How do I check the configuration version of the virtual machines running on Hyper-V? 

From an elevated command prompt, run the following command:

``` PowerShell
Get-VM * | Format-Table Name, Version

```


####Wie aktualisiere ich die Konfigurationsversion eines virtuellen Computers?

Führen Sie ein Windows PowerShell-Eingabeaufforderung einen der folgenden Befehle:

''' PowerShell
Update-VmConfigurationVersion < Vmname >


```

Or

``` PowerShell
Update-VmConfigurationVersion <vmobject>

```

** Wichtig: **

*   Nach der Aktualisierung der virtuellen Maschine Konfigurationsversion verschieben keine der virtuellen Maschine auf einem Host, die Windows 8.1 ausgeführt wird.
*   Die Version von Virtual Machine-Konfiguration von Version 6 auf Version 5 kann nicht heruntergestuft werden.
*   Sie müssen die virtuelle Maschine so aktualisieren Sie die Konfiguration des virtuellen Computers deaktivieren.
*   Nach dem Upgrade verwendet die virtuelle Maschine im neuen Dateiformat für die Konfiguration.
    Weitere Informationen finden Sie unter neue virtuelle Maschine Konfigurationsdateiformat.

##Neue virtuelle Maschine Konfigurationsdateiformat

Virtuelle Computer verfügen jetzt über ein neues Format für Konfiguration vorgesehen ist, um die Effizienz des lesen und Schreiben von Konfigurationsdaten für die virtuelle Maschine zu erhöhen.
Dieses Konzept auch potenzielle Datenverluste verringern, wenn Speicherausfalls vorhanden ist.
Die neue Konfiguration Dateien der. VMCX-Erweiterung für die Konfigurationsdaten für die virtuellen Computer und die. VMRS-Erweiterung für die Daten über den Laufzeitzustand.

> **Wichtig:** Die. VMCX-Datei ist ein binäres Format.
> Direktes Bearbeiten der. VMCX oder. VMRS Datei wird nicht unterstützt.
> 

##Integrationsservices, die über Windows Update bereitgestellt

Updates für die Integrationsdienste für Windows-basierte Gäste werden jetzt über Windows Update verteilt.

Integrationskomponenten (auch als Integrationsdienste bezeichnet) handelt es sich um den Satz von synthetische Treiber, die einen virtuellen Computer für die Kommunikation mit dem Hostbetriebssystem zu ermöglichen.
Dienste, die von der Synchronisierung bis hin zu Gast Dateikopie steuern.
Wir haben im Gespräch wurde für Kunden Komponenteninstallation Integration und Update im vergangenen Jahr erkennen können, dass sie während der Aktualisierung ein häufiger Problempunkt sind.

In der Vergangenheit Lieferumfang in allen neue Versionen von Hyper-V-Integrationskomponenten neue.
Aktualisieren des Hyper-V-Hosts erforderlich, die Integrationskomponenten auf den virtuellen Computern auch aktualisieren.
Die neue Integrationskomponenten wurden mit dem Hyper-V-Host, und klicken Sie dann sie auf den virtuellen Computern mit vmguest.iso installiert wurden.
Dieser Prozess neu gestartet werden muss der virtuellen Maschine und konnte nicht mit anderen Windows-Updates nicht als Batch verarbeitet werden.
Da der Hyper-V-Administrator hatte, vmguest.iso und die Administratoren mussten sie installieren anzubieten, erforderlich, Aktualisierung der Integration der Hyper-V-Administrator über Administratoranmeldeinformationen verfügen in den virtuellen Computern – was nicht immer der Fall.

Bearbeitet sowie andere wichtige Updates über Windows Update, Windows-10 und zukünftig alle Integration, Komponenten zu virtuell bereitgestellt werden.

Updates stehen für virtuelle Maschinen, heute verfügbar:

*   Windows Server 2012
*   Windows Server 2008 R2
*   Windows 8
*   Windows 7

Der virtuelle Computer muss Windows Update oder einem WSUS-Server verbunden sein.
In Zukunft müssen Komponentenupdates Integration eine Kategorie-ID in dieser Version, die sie als Knowledge Base-Artikel aufgelistet sind.

Weitere Informationen zu wie wir Anwendbarkeit ermitteln, finden Sie in diesem [Blogbeitrag](http://blogs.technet.com/b/virtualization/archive/2014/11/24/integration-components-how-we-determine-windows-update-applicability.aspx).

Unter [Dieser blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2014/11/12/updating-integration-components-over-windows-update.aspx) Stellen Sie eine ausführliche exemplarische Vorgehensweise für die Installation von Integrationsservices.

> **Wichtig:** Das ISO-Image-Datei vmguest.iso ist nicht mehr für das Aktualisieren von Integrationskomponenten erforderlich.
> Es ist nicht mit Hyper-V auf Windows 10 enthalten.
> 

##Als Nächstes

[Durchlaufen von Hyper-V auf Windows 10](..\quick_start\walkthrough.md)


