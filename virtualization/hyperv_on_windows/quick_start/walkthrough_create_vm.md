MS. ContentId: 3C63F9A8-30E4-40F4-BC7B-A001C1E90779
Titel: Schritt 4: Erstellen Sie eine virtuellen Windows-Maschine aus einer ISO-Datei

#Schritt 4: Erstellen Sie eine virtuellen Windows-Maschine aus einer ISO-Datei

Für diesen Schritt Wenn bereits eine .iso-Datei für einen unterstützten 64-Bit-Betriebssystem können, das Sie.
Wenn dies nicht der Fall ist, können Sie die .iso für herunterladen [Windows 8.1 Enterprise](http://www.microsoft.com/en-us/evalcenter/evaluate-windows-8-1-enterprise) und wählen Sie die 64-Bit-Edition.

1.  Klicken Sie im Hyper-V-Manager auf der **Aktion** Menü > **Neu** > **Virtueller Computer**.
2.  Stellen Sie in der Virtual Machine-Assistenten die folgenden Optionen:
    
    <table>
      <tr>
        <th caps_internal_Id="b32cba15-e0ca-4edf-9f3c-acc882ff8344">Page</th>
        <th caps_internal_Id="19410809-def1-4df4-9524-4a5f79f12ef2">Entry</th>
      </tr>
      <tr>
        <td caps_internal_Id="43cbc3a2-80b7-439f-8220-1b23a7c15910">Name:</td>
        <td>Type in <b caps_internal_Id="523822ab-2bd6-4599-9e14-36d0251f7a26">Windows Walkthrough VM</b></td>
      </tr>
      <tr>
        <td caps_internal_Id="a47fbf80-9877-49f6-904f-40f1c15703e5">Generation:</td>
        <td>
          <b caps_internal_Id="2e2117bb-37c7-47a9-b996-3ec57bbe4223">Generation 2</b>
        </td>
      </tr>
      <tr>
        <td caps_internal_Id="92f42acc-fa5e-41a3-aa96-d2a0d3ef2359">Startup Memory:</td>
        <td>
          <b caps_internal_Id="f7bc1548-427a-4b19-b61f-1915c21fad89">1024</b> and leave dynamic memory selected</td>
      </tr>
      <tr>
        <td caps_internal_Id="42a32f67-bc64-44b7-8a71-638e5816bf45">Configure Networking:</td>
        <td>
          <b caps_internal_Id="fc76cab1-090f-4bb4-844b-23533b874cfe">External</b> (this is the virtual switch you created in Step 3)</td>
      </tr>
      <tr>
        <td caps_internal_Id="55ad9abc-3317-4569-8d6e-c62a687fb5f7">Connect virtual hard disk:</td>
        <td>
          <b caps_internal_Id="5475798c-6a3e-4c19-b331-55c6480ea45f">Create a virtual hard disk</b> (keep the other default values) </td>
      </tr>
      <tr>
        <td caps_internal_Id="bf7e5cb2-0c83-426b-8ac2-49b8fc6db155">Installation Options:</td>
        <td>
          <b caps_internal_Id="52b190d3-efcf-4a91-ace3-69b86f7df7c2">Install an operating system from a bootable CD/DVD-ROM</b>. Under <b caps_internal_Id="3f569bd8-5fb2-48b6-8722-dfe1cd64d91c">Media</b>, select <b caps_internal_Id="dcc18df8-66cb-40bc-aae9-d29a576cef28">Image file (iso)</b> and then click <b caps_internal_Id="9924023d-10ac-45c5-b06c-ebc14aced20e">Browse</b> to point to the .iso file.</td>
      </tr>
    </table>
3.  Wenn alles wie gewünscht aussieht, klicken Sie auf **Fertig stellen**.

> **Hinweis:** Wenn Sie nur 32-Bit-Version von Windows haben, müssen Sie auf Generation 1 in der **Generation** Der Abschnitt des Assistenten.
> VMs Generation 2 unterstützen nur 64-Bit-Betriebssysteme.
> 

##Nächster Schritt:

[Schritt 5: Herstellen einer Verbindung mit dem virtuellen Computer, und schließen Sie die installation](walkthrough_vmconnect.md)


