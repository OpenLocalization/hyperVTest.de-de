MS. ContentId: 95FE9554-3968-4EED-B65D-E03F06A7598D
Titel: „Schritt 3: Erstellen eines virtuellen Switch

#„Schritt 3: Erstellen eines virtuellen Switch

Ein virtueller Switch können Sie eine Netzwerkschnittstelle für den virtuellen Computer zu erstellen.
Sie werden wie der Netzwerkadapter (NIC) auf dem physischen Computer verwendet.

In diesem Beispiel werden wir einen externen Switch erstellen.
Der externe Switch ermöglicht Ihrem virtuellen Computer Zugriff auf den Host Netzwerkadapter des Computers.
Wenn der Hostcomputer mit dem Internet verbunden ist, werden den virtuellen Computer auch.

Wir müssen auch den Schalter ermöglicht es den Host, gemeinsames Verwenden dieses Netzwerkadapters festlegen.
Dies macht es also sowohl die virtuellen Maschinen und Hosts kann im selben Netzwerk.


1.  Klicken Sie im Hyper-V-Manager auf **Manager für virtuelle Switches**.
    
    !(media/virtual_switch_manager1.png)
2.  Wählen Sie **Neues virtuelles Netzwerk-switch**.
    
    !(media/new_switch.png)
3.  Wählen Sie **Extern** und **Virtuellen Switch erstellen**.
    
    !(media/new_switch_createbutton.png)
4.  Klicken Sie unter **Name**geben Sie Folgendes ein: **Extern**.
5.  Klicken Sie unter **Externes Netzwerk**, wählen Sie den richtigen Netzwerkadapter (es wird wahrscheinlich nur eine Option sein).
6.  Wählen Sie **Lassen Sie gemeinsames Verwenden dieses Netzwerkadapters Verwaltungsbetriebssystem zu** , und klicken Sie auf **OK**.
    
    !(media/share_nic.png)
7.  Sie erhalten eine Meldung darüber angezeigt, dass Ihr Netzwerk während der Erstellung des virtuellen Switches trennt.
    Klicken Sie einfach auf **Ja**.
    Ihr Netzwerk wird für kurze Zeit nicht verfügbar sein.
    
    !(media/network_warning.png)

##Nächster Schritt:

[Schritt 4: Erstellen Sie eine virtuellen Windows-Maschine aus einer ISO-Datei](walkthrough_create_vm.md)


