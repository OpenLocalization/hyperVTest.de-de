MS. ContentId: B971C429-CEF0-4DAB-8456-3B08AEC0C233
Titel: Schritt 7: Exportieren und Importieren eines virtuellen Computers

#Schritt 7: Exportieren und Importieren eines virtuellen Computers

Können Sie schnell einen virtuellen Computer kopieren oder verschieben ein virtuellen Computers mit den Export und Funktionalität zu importieren.

##Exportieren des virtuellen Computers

Exportieren einer virtuellen Maschine exportiert alle Bestandteile des virtuellen Computers, einschließlich der Prüfpunkte.

1.  In Hyper-V-Manager mit der rechten Maustaste in den virtuellen Computer, und wählen Sie **Exportieren**.
    
    !(media/select_export1.png)
2.  Klicken Sie im Menüband auf **Durchsuchen** Klicken Sie im Dialogfeld Feld und navigieren Sie zu C:\Users\Public aus, und klicken Sie dann auf **Wählen Sie Ordner**.
3.  Klicken Sie im Abschnitt **Exportieren der virtuellen Maschine** Dialogfeld, stellen Sie sicher, dass der Pfad sieht dies kein Problem, und klicken Sie dann auf **Exportieren**.
    
    !(media/click_export.png)
4.  Während der virtuelle Computer exportiert werden, können Sie den Fortschritt im Abschnitt Status finden Sie unter:
    
    !(media/export_progress.png)

##Werden der Export wurde ausgeführt?

Um sicherzustellen, dass der virtuelle Computer exportiert wurde, der rechten Maustaste auf Ihre **Starten Sie** im Menü **Datei-Explorer**.

1.  Navigieren Sie zu C:\Users\Public\Windows Exemplarische Vorgehensweise VM.
2.  Einen anderen Ordner namens Windows Exemplarische Vorgehensweise VM und in diesem Ordner sollte drei Ordner mit den Dateien für den exportierten virtuellen Computer sollte angezeigt werden:
    
    *   Momentaufnahmen
    *   Virtuelle Festplatten
    *   Virtuelle Computer 
    
    !(media/export_confirm.png)

##Die virtuellen Computer importieren

Bevor wir den virtuellen Computer importieren, werden wir den ursprünglichen virtuellen Computer löschen.
Mit der rechten Maustaste auf den virtuellen Computer, und wählen **„Löschen“**.

1.  In **Hyper-V-Manager**, in der **Aktion** auf **Virtuellen Computer importieren**.
2.  Klicken Sie im Abschnitt **Ordner suchen** im Abschnitt, klicken Sie auf Durchsuchen und navigieren Sie zu C:\Users\Public\Windows Exemplarische Vorgehensweise VM und klicken Sie dann auf **Weiter**.
3.  Klicken Sie im Abschnitt **Wählen Sie die virtuellen Computer importieren** Bildschirm auf **Weiter**.
4.  Klicken Sie im Abschnitt **Importtyp auswählen** Wählen Sie im Abschnitt **Registrieren Sie den virtuellen Computer an** und klicken Sie dann auf **Weiter**.
5.  Klicken Sie im Abschnitt **Ziel auswählen** im Abschnitt, behalten Sie die Standardeinstellung, und klicken Sie auf **Weiter**.
6.  Lassen Sie in Ordnern Speicher auswählen den Standardpfad, und klicken Sie auf **Weiter**.
7.  Klicken Sie auf der Seite "Zusammenfassung" sehen eine Liste der Pfade Sie, wo die neuen VM-Dateien gespeichert werden sollen.
    Klicken Sie im Menüband auf **Fertig stellen** um den Importvorgang zu starten.

##Werden der Import wurde ausgeführt?

Stellen Sie sicher, dass der Import erfolgreich war, doppelklicken Sie einfach auf den virtuellen Computer im **Hyper-V-Manager** und starten Sie VMConnect, um den virtuellen Computer zu überprüfen.

##Nächster Schritt:

[Schritt 8: Experimentieren Sie mit WindowsPowerShell](walkthrough_powershell.md)


