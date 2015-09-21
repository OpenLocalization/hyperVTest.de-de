MS. ContentId: FBBAADE6-F1A1-4B5C-8FD2-BDCA3FCF81CA
Titel: Schritt 6: Experimentieren Sie mit Prüfpunkten

#Schritt 6: Experimentieren Sie mit Prüfpunkten

Prüfpunkte sind hilfreich, wenn Sie den aktuellen Zustand einer virtuellen Maschine zu speichern, bevor Sie eine Änderung wie z. B. eines Updates, Software installieren oder eine Einstellung ändern möchten.
Falls die Änderung Probleme verursacht, können Sie den Prüfpunkt wiederherstellen und zurück.

Es gibt zwei Typen von Prüfpunkten:  
**Produktion Prüfpunkte**: Vor allem auf Servern in produktionsumgebungen verwendet.
**Standard-Prüfpunkte**: In der Entwicklung oder Tests Umgebungen verwendet

Produktions-Prüfpunkte werden standardmäßig für Hyper-V auf Windows-10.

##Ändern Sie den prüfpunkttyp

Wir beginnen mit der älteren Prüfpunkte ausprobieren, **Standard-Prüfpunkte**.
Da Produktion Prüfpunkten konfiguriert wurden, müssen wir ein Wechsel in den Einstellungen für den virtuellen Computer, und ändern Sie den prüfpunkttyp.

1.  Mit der rechten Maustaste auf **Exemplarische Vorgehensweise Windows-VM** und wählen Sie **Einstellungen**.
2.  Klicken Sie im Abschnitt **Verwaltung** Wählen Sie im Abschnitt **Prüfpunkte**.
3.  Wählen Sie **Standard-Prüfpunkte**.
    Das Dialogfeld sollte wie folgt aussehen:
    
    !(media/standard1.png)
4.  Klicken Sie im Menüband auf **OK** um das Dialogfeld zu schließen.

##Öffnen Sie den Editor zum Testen von Prüfpunkten

Um zu sehen, was geschieht, mit jeder Art von Checkpoint, erhalten wir eine Anwendung auf dem virtuellen Computer ausgeführt.

1.  Mit der rechten Maustaste auf **Exemplarische Vorgehensweise Windows-VM** und wählen Sie **Verbinden Sie**.
2.  Öffnen Sie in der virtuellen Maschine **Editor** durch Klicken auf die **Starten Sie** Menü und eingeben **Editor** und wählen sie aus den Ergebnissen.
3.  Geben Sie im Editor **Dies ist ein Test von Prüfpunkten.** Die Datei sollte wie folgt aussehen:
    
    !(media/standard_notepad.png)
4.  Speichern Sie die Datei **Test.txt**, aber schließen Sie Editor nicht.
    Lassen sie auf dem virtuellen Computer ausgeführt wird.

##Erstellen Sie einen standard-Prüfpunkt

1.  Um den Prüfpunkt zu erstellen, klicken Sie auf der !(media/checkpoint_button.png)**Checkpoint** die Schaltfläche in der Menüleiste.
2.  Geben Sie im Dialogfeld für die Prüfpunkt-name **Standard**.
    Das Dialogfeld sollte wie folgt aussehen:
    
    !(media/save_standard.png)
3.  Wenn der Prozess abgeschlossen ist, wird der Prüfpunkt unter angezeigt. **Prüfpunkte** in der **Hyper-V-Manager**.
    
    !(media/standard_complete.png)

##Erstellen Sie einen Prüfpunkt für die Produktion

Wir müssen jetzt ändern, ändern Sie den Typ des Prüfpunkts, die wir wieder zu übernehmen möchten. **Produktion Prüfpunkte** vor dem Erstellen eines zweiten Prüfpunkts.

1.  Mit der rechten Maustaste in den virtuellen Computer, und klicken Sie auf **Einstellungen**.
2.  Klicken Sie im Abschnitt **Verwaltung** Wählen Sie im Abschnitt **Prüfpunkte**.
3.  Wählen Sie **Produktion Prüfpunkte**.
4.  Deaktivieren Sie die Herbst-Back-Option.
    Wenn das System einen Prüfpunkt für die Produktion nicht akzeptiert werden, möchten wir, anstatt einen standard-Prüfpunkt nicht ausgeführt.
    
    !(media/production.png)
5.  Klicken Sie auf **OK** um das Dialogfeld zu schließen.
6.  Mit der rechten Maustaste auf den virtuellen Computer erneut, und wählen Sie **Verbinden Sie**.
7.  Geben Sie im Editor auf dem virtuellen Computer eine andere Zeile **Dies ist ein Test einen Prüfpunkt für die Produktion** und speichern Sie die Datei erneut.
8.  Klicken Sie auf der !(media/checkpoint_button.png)**Checkpoint** die Schaltfläche in der Menüleiste.
9.  Wenn Sie gefragt werden, nennen Sie es **Production um** und klicken Sie dann auf **Ja**.
    
    !(media/production_CheckpointName.png)
10.  VMConnect zu schließen.
    Die VM wird weiter ausgeführt, Sie einfach wird nicht verbunden sein, nicht mehr.
11.  In Hyper-V-Manager wird die Liste der Prüfpunkte nun wie folgt aussehen:
    
    !(media/production_complete.png)

##Den standard-Prüfpunkt anwenden

1.  In **Hyper-V-Manager**, in der **Prüfpunkte** im Abschnitt der rechten Maustaste auf den Titel einer **Standard** , und klicken Sie auf **Übernehmen**.
2.  Klicken Sie im Popup-Dialogfeld auf **Prüfpunkt erstellen und anwenden**.
    
    !(media/apply_standard.png)
3.  Wenn abgeschlossen ist, die Liste der Prüfpunkte nun wird etwa folgendermaßen aussehen:
    
    !(media/standard_applied.png)
4.  Wenn dies abgeschlossen ist der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf **Verbinden Sie** Verbinden mit dem virtuellen Computer.
5.  Beim Herstellen einer mit dem virtuellen Computer Verbindung des virtuellen Computers ausgeführt werden sollte, mit dem Editor öffnen, aber die Zeile zu Produktion Prüfpunkte fehlen:
    
    !(media/standard_applied_notepad.png)
6.  Schließen Sie VMConnect, und lassen Sie den virtuellen Computer ausgeführt.

##Den Prüfpunkt für die Produktion übernehmen

Nun wechseln wir wieder zu Hyper-V-Manager gelten des Produktions-Prüfpunkts und sehen, wie die virtuellen Computer anschließend aussieht.

1.  Klicken Sie im Abschnitt Prüfpunkte Maustaste diejenige mit dem Titel **Produktion Prüfpunkt** , und klicken Sie auf **Übernehmen**.
2.  Wählen Sie im Popup-Dialogfeld **Prüfpunkt erstellen und anwenden**.
3.  Wenn dies abgeschlossen ist der rechten Maustaste auf den virtuellen Computer, und klicken Sie auf **Verbinden Sie** um den virtuellen Computer zu starten.
4.  Sie werden feststellen, dass der virtuelle Computer nicht ausgeführt wird.
    Klicken Sie auf der !(media/start.png) Schaltfläche "Start" in der Menüleiste, um den virtuellen Computer zu starten.
5.  Öffnen Sie im Editor geöffneten test.txt.
    Die Zeile in der Datei zum Testen der Produktion Prüfpunkte sollte angezeigt werden:
    
    !(media/production_notepad.png)

##Umbenennen eines Prüfpunkts

1.  Mit der rechten Maustaste in des letzten Prüfpunkts in der Struktur, und klicken Sie auf Umbenennen.
2.  Name des Prüfpunkts **Löschen Sie mich**.
    
    !(media/delete_me.png)

##Löschen eines Prüfpunkts

Im vorherige Schritt wurde wahrscheinlich erhalten Sie einen Hinweis weiter wir.
Wir werden den Prüfpunkt zu löschen, den Sie gerade umbenannt.

1.  Mit der rechten Maustaste auf den Prüfpunkt namens **Löschen Sie mich** , und klicken Sie auf **Prüfpunkt löschen**.
    
    !(media/delete_checkpoint.png)
2.  Klicken Sie im Dialogfeld mit Warnung auf **„Löschen“**.
    
    !(media/delete_warn.png)
3.  Nachdem der Prüfpunkt gelöscht wurde, sollte die Liste etwa folgendermaßen aus:
    
    !(media/after_delete.png)

##Nächster Schritt:

[Schritt 7: Exportieren und Importieren eines virtuellen Computers](walkthrough_export_import.md)


