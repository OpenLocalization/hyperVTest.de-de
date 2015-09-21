MS. ContentId: A6DD6776-614C-4D28-9B83-CB2EDFD263A3
Titel: Schritt 2: Installieren Sie Hyper-V auf Windows 10

#Schritt 2: Installieren Sie Hyper-V auf Windows 10

Hyper-V kann mit installiert werden [Programme und Funktionen](#UsingProgramsandFeatures) oder [WindowsPowerShell](#UsingPowerShell).

##Über die Programme und Funktionen

1.  Klicken Sie mit der rechten Maustaste auf **Windows** Schaltfläche, und klicken Sie dann auf **Programme und Funktionen**.
    
    !(media\programs_and_features.png)
2.  Klicken Sie im Menüband auf **Aktivieren Sie oder deaktivieren Sie Windows-features**.
3.  Wählen Sie **Hyper-V**und anschließend auf **OK**
    
    !(media\hyper-v_feature_selected.png)
4.  Wenn die Installation abgeschlossen ist, müssen Sie den Computer neu starten.
    
    !(media\restart.png)

##Mithilfe von PowerShell

Weitere Informationen finden Sie in der PowerShell-Hilfe für [Enable-WindowsOptionalFeature](https://technet.microsoft.com/library/hh852172.aspx).

1.  Klicken Sie auf der **Windows** Schaltfläche "und" Suchen **Windows PowerShell**.
2.  Mit der rechten Maustaste auf **Windows PowerShell** und klicken Sie dann auf **Als Administrator ausführen**.
3.  Windows-Powerhshell aufgefordert werden, geben Sie Folgendes ein, und drücken Sie dann die **EINGABE** Schlüssel:  
    ` PowerShell
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
    `
4.  Wenn die Installation abgeschlossen ist, starten Sie den Computer neu.

##Wie weiß ich Hyper-V ordnungsgemäß installiert?

Nachdem Sie Ihre Computer starten das Tool Hyper-V-Manager neu gestartet.

1.  Klicken Sie auf der **Windows** Schaltfläche und Typ **Hyper-V**.
2.  Klicken Sie auf **Hyper-V-Manager** in der Liste.
3.  Die Hyper-V-Manager-Anwendung startet.

##Als Nächstes

[„Schritt 3: Erstellen eines virtuellen Switch](walkthrough_virtual_switch.md)


