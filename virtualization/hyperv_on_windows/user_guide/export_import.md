MS. ContentId: 040B1B51-0F25-4295-B317-8CC4DE0A1AFF
Titel: Exportieren und Importieren von virtuellen Computern


#Exportieren und Importieren von virtuellen Computern

Sie können mithilfe der Export und Importieren von Funktionen können Sie virtuelle Computer schnell duplizieren oder von einem Host auf einen anderen verschieben.
Sie müssen nicht Exportieren eines virtuellen Computers, damit es importiert werden.
Sie können einfach einen virtuellen Computer und die zugehörigen Dateien auf dem neuen Host kopieren und dann die **Virtuellen Computer importieren** Assistenten, um den Speicherort der Dateien anzugeben.
Dadurch wird der virtuelle Computer mit Hyper-V registriert und es können verwendet werden.

##Exportieren von virtuellen Maschinen

Eine einfache Möglichkeit zum Vorbereiten von virtuellen Maschinen zu importierenden ist die **Exportieren der virtuellen Maschine** Assistenten.

1.  In Hyper-V-Manager wählen Sie eine oder mehrere virtuelle Computer mit der rechten Maustaste auf die Auswahl, und wählen Sie **Exportieren**.
2.  Klicken Sie im Menüband auf **Durchsuchen** Klicken Sie im Dialogfeld ein, und wählen Sie, wo Sie möchten den exportierten VMs und dann auf **Wählen Sie Ordner**.
3.  Klicken Sie im Abschnitt **Exportieren der virtuellen Maschine** im Dialogfeld klicken Sie auf **Exportieren**.

Informationen zur Verwendung von Windows PowerShell zum Exportieren von virtuellen Maschinen finden Sie unter [Export-VM](https://technet.microsoft.com/library/hh848491.aspx)

##Importieren von virtuellen Computern

1.  In **Hyper-V-Manager**, in der **Aktion** auf **Virtuellen Computer importieren**.
2.  Klicken Sie im Abschnitt "Ordner suchen" auf Durchsuchen, und navigieren Sie, in dem Dateien der virtuellen Maschine befinden.
    <!--zum Überprüfen der aufgelösten - dieses Verhalten ist dies einen Fehler aus meiner Sicht--> Bitte beachten Sie, dass mithilfe des Assistenten können einen virtuellen Computer zu einem Zeitpunkt importieren und die VM-Ordner anstatt auf den Exportordner Allgemein auswählen.
    Klicken Sie im Menüband auf **Weiter** Wenn abgeschlossen ist.
3.  Wählen Sie die virtuellen Computer importieren, und klicken Sie dann auf **Weiter**.
4.  Im Abschnitt Importtyp auswählen können Sie den virtuellen Computer importieren auswählen:
    
    *   **Registrieren** – Verwendet die vorhandene eindeutige ID des virtuellen Computers und registriert sie direkte.
        Wählen Sie diese Option, wenn sich die Dateien des virtuellen Computers bereits am richtigen Speicherort befinden.
    *   **Wiederherstellen** – Verwendet die eindeutige ID für den ursprünglichen virtuellen Computer und auch eine Kopie die Dateien für virtuelle Maschinen am Standardspeicherort für den Host angegeben.
    *   **Kopieren** -Erstellt eine neue eindeutige ID für den virtuellen Computer und auch eine Kopie die Dateien der virtuellen Maschine am Standardspeicherort für den Host angegeben.
5.  Klicken Sie nach der Auswahl des virtuellen Computers zu importieren auf **Weiter**.
6.  Im Abschnitt Ziel auswählen können Sie auswählen, wo die Dateien für den virtuellen Computer speichern, oder lassen Sie sie in ihrem aktuellen Speicherort.
    Wenn Sie fertig sind, klicken Sie auf **Weiter**.
7.  In Ordnern Speicher auswählen können Sie ein anderer Ort für die vhdx-Datei zu speichern, oder lassen sie auswählen, wo sie sind.
    Wenn Sie fertig sind, klicken Sie auf **Weiter**.
8.  Wenn Sie mit dem Importieren des virtuellen Computers abgeschlossen haben, sehen Sie die Seite "Zusammenfassung", die beschreibt, wo sich die neuen VM-Dateien befinden.

Der virtuellen Computer importieren-Assistent führt Sie auch über die Schritte zum Adressieren von Inkompatibilitäten beim Importieren der virtuellen Maschine auf dem neuen Host, damit dieser Assistent bei Konfiguration helfen kann, die physische Hardware, wie z. B. Arbeitsspeicher, virtuelle Switches und virtuelle Prozessoren zugeordnet ist.

Beim Import eines virtuellen Computers führt der Assistent die folgenden Schritte aus:

1.  Er erstellt eine Kopie der Konfigurationsdatei des virtuellen Computers.
    Dies ist eine Vorsichtsmaßnahme für den Fall, dass der Host beispielsweise aufgrund eines Stromausfalls außerplanmäßig neu gestartet wird.
2.  Er überprüft die Hardware.
    Die Informationen in der Konfigurationsdatei des virtuellen Computers werden mit der Hardware des neuen Hosts verglichen.
3.  Er erstellt eine Fehlerliste.
    Diese Liste zeigt auf, wo Konfigurationsbedarf besteht, und bestimmt somit, welche Assistentenseiten als nächstes angezeigt werden.
4.  Zeigt die relevanten Seiten, einer Kategorie zu einem Zeitpunkt.
    Der Assistent wird erläutert, jede Inkompatibilität, mit denen Sie den virtuellen Computer neu konfigurieren, damit er mit dem neuen Host kompatibel ist.
5.  Er entfernt die Kopie der Konfigurationsdatei.
    Danach kann der virtuelle Computer gestartet werden.

Statt des Assistenten können Sie auch die Cmdlets des Hyper-V-Moduls für Windows PowerShell zum Importieren virtueller Computer verwenden.
Weitere Informationen finden Sie unter [Import-VM](https://technet.microsoft.com/library/hh848495.aspx).


