MS. ContentId: 7dcd6da0-dd72-422d-8752-5eccc8116e02
Titel: Verwalten von remote Hyper-V-hosts

#Verwalten von Remote-Hyper-V-Hosts mit Hyper-V-Manager

Hyper-V-Manager stellt Tools für die Diagnose und Verwaltung Ihrer lokalen Hyper-V-Hosts und eine kleine Anzahl von Remotehosts.
Dieser Artikel beschreibt die Konfigurationsschritte für die Verbindung mit der Hyper-V-Hosts mit Hyper-V-Manager in allen unterstützten Konfigurationen.

Stellen Sie sicher, dass zum Verbinden mit einem Hyper-V-Host im Hyper-V-Manager **Hyper-V-Manager** Klicken Sie im linken Bereich ausgewählt ist und anschließend aktivieren **Verbindung mit Server herstellen...** im rechten Bereich.

!(media/HyperVManager-ConnectToHost.png)

##Unterstützte Kombinationen von Hyper-V-Host mit Hyper-V-Manager

Hyper-V-Manager in Windows 10 können Sie verwalten:

*   Windows-10
*   Windows 8.1 und Windows Server 2012 R2 Hyper-V-hosts
*   Windows 8 und Windows 2012 Hyper-V-hosts

Hyper-V-Manager in Windows 8.1 und Windows Server 2012 R2 können Sie verwalten:

*   Windows 8.1 und Windows Server 2012 R2 Hyper-V-hosts
*   Windows 8 und Windows 2012 Hyper-V-hosts

> **Hinweis:** Nicht alle Funktionen von Hyper-V-Manager funktioniert für alle hostversionen.
> 

##Verwalten von "localhost"

Wählen Sie "localhost" Hyper-V-Manager als Hyper-V-Host hinzu, **Lokaler computer** in der **Computer auswählen** Dialog Box.

!(media/HyperVManager-ConnectToLocalHost.png)

Wenn eine Verbindung hergestellt werden kann:

*   Stellen Sie sicher, dass die Hyper-V-Serverrolle aktiviert ist.
    Finden Sie in der [Exemplarische Vorgehensweise im Abschnitt für die Überprüfung der Kompatibilität](../quick_start/walkthrough_compatibility.md).
*   Vergewissern Sie sich, dass Ihr Benutzerkonto der Gruppe der Hyper-V-Administratoren gehört.

##Verwalten von einem Hyper-V-Host in der Domäne

Wählen Sie zum Hinzufügen einer Hyper-V-Remotehost zu Hyper-V-Manager **Einem anderen computer** in der **Computer auswählen** Dialog Box, und geben Sie des Remotehosts Hostnamen, NetBIOS oder FQDN in das Textfeld ein.

!(media/HyperVManager-ConnectToRemoteHost.png)

Stark erweitert Windows 10 möglichen Kombinationen von Remoteverbindung Typen.
Jetzt können Sie auf einem remote-Windows-10 oder höher Host, der den Hostnamen oder die IP-Adresse verbinden.
Hyper-V-Manager unterstützt jetzt auch alternative Anmeldeinformationen.

Um remote Hyper-V-Hosts zu verwalten, muss die Remoteverwaltung auf beiden Computern aktiviert sein.

Hierzu können Sie durch `System Properties -> Remote Management Settings` oder durch Ausführen das folgende PowerShell Befehl als Administrator aus:  

` PowerShell
winrm quickconfig
`

Wenn Ihr aktuelles Benutzerkonto ein Hyper-V-Administratorkonto auf dem Remotehost übereinstimmt, fahren Sie fort, und drücken Sie die **OK** Verbinden.

Dies ist die einzige unterstützte Möglichkeit zum Verwalten von eines Remotehosts in Hyper-V-Manager in Windows 8 oder Windows 8.1.

###Verbindung zum remote-Host als anderer Benutzer

In Windows-10 Wenn Sie nicht mit dem richtigen Konto für den remote-Host ausführen können Sie als ein anderer Benutzer mit alternativen Anmeldeinformationen verbinden.

Wählen Sie zum Angeben von Anmeldeinformationen für den Remoteserver Hyper-V-host **Verbinden Sie sich als ein anderer Benutzer: ** in der ** Computer auswählen** Wählen Sie dann im Dialogfeld Feld **Benutzer werden festgelegt...**.

!(media/HyperVManager-ConnectToRemoteHostAltCreds.png)

> Hinweis:  Es ist sehr leicht vergessen, den Benutzer und klicken Sie auf OK, mit der Benutzer nicht angegeben.
> Wenn die Verbindung fehlschlägt, stellen Sie sicher, dass Sie tatsächlich vom Benutzer festgelegt.
> 

###Herstellen einer Verbindung mit dem Remotehost über IP-Adresse

Manchmal ist es einfacher, eine Verbindung über IP-Adresse anstelle der Host-Name.
Windows-10 bietet die genau dies.

Um mit der IP-Adresse zu verbinden, geben Sie die IP-Adresse in der **Einem anderen Computer** Text-Feld.

##Verwalten einer Hyper-V-Hosts außerhalb der Domäne (oder keine Domäne)

<!--vorausgesetzt, dies ist nicht noch fertig... erneut Anforderungen Kontext.-->
Lokaler Hyper-V-Host:

1.  Enable-PSRemoting
    Kam wieder mit öffentlichen Netowork.
    Ausgeführt wurde
    Set-NetConnectionProfile-Namen "Name" - NetworkCategory privat
2.  Set-Item WSMan:\localhost\Client\TrustedHosts *-Force
3.  Enable-WSManCredSSP-Rolle Client - DelegateComputer *

Für Arbeitsgruppen:

1.  (sollte erfolgen) Computer Computerrichtlinie\Administrative Templates\System\Credentials Delegation\Allow delegieren aktuelle Anmeldeinformationen → auf aktiviert festgelegt und Hinzufügen von WS-Management / *].
    Überprüfen Sie zur Liste der Computer im ForConcatenate Betriebssystem standardmäßig mit den oben genannten Eingabe
2.  Computer Computerrichtlinie\Administrative Templates\System\Credentials Delegation\Allow delegieren aktuelle Anmeldeinformationen mit reiner NTLM-Serverauthentifizierung → auf aktiviert festgelegt und Hinzufügen von WS-Management / * eine Liste von Computern, aktivieren Sie das Kontrollkästchen Verketten von OS-Standards mit der Eingabe, die oben genannten
3.  Computer Computerrichtlinie\Administrative Vorlagen\Windows-Komponenten\Windows-Remoteverwaltung (WinRM) \WinRM Client\Allow CredSSP-Authentifizierung → auf aktiviert festgelegt

Remote-Hyper-V-Host:

1.  Die Firewall deaktiviert :)
2.  Enable-PSRemoting
3.  Set-Item WSMan:\localhost\Client\TrustedHosts *-Force
    Das ist also nur Demo-Anweisungen verwendet.
    Ersetzen Sie * Firewall mit einem einzelnen Computer deaktivieren, und lassen Sie Credssp und WinRM über


