MS. ContentId: C2593EA1-B182-4C71-8504-49691F619158
Titel: Schritt 1: Stellen Sie sicher, dass Ihr Computer kompatibel ist.

#Schritt 1: Sicherstellen Sie, dass Ihr Computer Hyper-V ausgeführt werden können

Nur Windows 10 Pro und Windows 10 Enterprise unterstützen Hyper-V.

> Wenn Sie Windows 10 Home – ausführen können Sie in der Aktivierungsseite befindet sich in den Sicherheitseinstellungen für gewinnen 10 pro aktualisieren.
> Über den Link "Gehe zum Speichern von" gelangen Sie zu einer Seite zum Aktualisieren.
> 

Hyper-V ist nicht verfügbar in Windows 10 Mobile / Windows 10 Mobile Enterprise

Hyper-V erfordert mindestens 4 GB RAM, aber Sie möglicherweise mehr benötigen, wenn Sie mehrere virtuelle Computer gleichzeitig ausführen möchten.

Ab Windows 10 ist Hyper-V einen 64-Bit-Prozessor mit Second Level Address Translation (SLAT) erforderlich.

##Vergewissern Sie sich Hardware-Kompatibilität

Öffnen Sie zum Überprüfen der Kompatibilität mit PowerShell oder Windows-Befehlszeile (cmd.exe) und Typ: `systeminfo.exe`.
Dadurch erhalten Sie Informationen zu Ihrem Computer.

Alle Elemente unter **Anforderungen für Hyper-V** den Wert benötigen Wenn **Ja**.

!(media\systeminfo.png)

Relevante Abschnitte:

*   `OS Name` – Windows 8 oder höher und entweder Beruf oder Enterprise erforderlich.
*   `Hyper-V Requirements` – Alle diese muss "true" (Wert "Yes"), aber einige im BIOS konfiguriert werden können.
    
    *   `VM Monitor Mode Extensions` ---Eigenschaft der Hardware.
        Hyper-V kann auf diesem Computer nicht ausgeführt.
    *   `Virtualization Enabled in Firmware` --Können im BIOS aktiviert sein
    *   `Second Level Address Translation` ---Eigenschaft der Hardware.
        Hyper-V kann auf diesem Computer nicht ausgeführt.
    *   `Data Execution Prevention Available` --Können im BIOS aktiviert sein

Wenn Hyper-V bereits aktiviert ist, liest der Anforderungen für Hyper-V-Abschnitt:  


```
Hyper-V Requirements: A hypervisor has been detected. Features required for Hyper-V will not be displayed.

```


##Nächster Schritt:

[Schritt 2: Installieren von Hyper-V](walkthrough_install.md)


