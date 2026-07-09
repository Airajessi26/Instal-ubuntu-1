jika menginsta genieacs sudah berhasil selanjutnya menambahkan parameter 

1. ke genieACS ke menu admin lalu config di edit index page masukan perintah untuk menambahkan parametres 

  contoh perintah yang di masukan 
  
    - label: "'Tag'"
      parameter: Tags
      type: "'tags'"
    - label: "'Action'"
      type: "'summon-button'"
    - element: "'span.inform'"
      label: "'Status'"
      parameter: DATE_STRING(Events.Inform)
      type: "'container'"
      components:
        - type: "'parameter'"
        - chart: "'online'"
          type: "'overview-dot'"
    - label: "'SSID'"
      parameter: InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID
    - label: "'RXPower'"
      parameter: VirtualParameters.rx_power
    - label: "'Uptime'"
      parameter: VirtualParameters.uptime
    - label: "'Secreat PPPoE'"
      parameter: VirtualParameters.secreat_PPPoE
    - label: "'IP WAN/TR069'"
      parameter: InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANPPPConnection.3.ExternalIPAddress
    - label: "'SN ONT'"
      parameter: DeviceID.SerialNumber
    - label: "'PON Type'"
      parameter: InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.WANAccessType
      type: "'device-link'"
      components:
        - type: "'parameter'"
    - Parameter: VirtualParameter.GetPONMode
    
  lalu seav untuk menyimpan perintah yang telah kita buat
    
  ambil salah 1 parameters dari salah 1 modem yang telah di koneksikan ke genieacs, tetapi karena setiap modem tidak selalu sama parameternya jadi kita harus memberikamn perintah yang berbeda

2. selanjutnya masuk ke menu >admin lau ke menu > virtual parameters > New
        
  contoh perintah (secrip) yang di berikan :
  
  🖋️perintah (secrip) ip untuk memunculkan keterangan ip dalam setiap modem di genieacs

  🖋️isi name nya contoh (IPWAN_TR09)

    const now = Date.now();
    
    let r1 = declare("InternetGatewayDevice.WANDevice.*.WANConnectionDevice.*.WANPPPConnection.*.ExternalIPAddress", {value: 1});
    let r2 = declare("InternetGatewayDevice.WANDevice.*.WANConnectionDevice.*.WANPPPConnection.*.ExternalIPAddress", {value: 1});
    let r3 = declare("Device.IP.Interface.*.IPv4Address.*.IPAddress", {value: 1});
    
    let ip = (r1 && r1.size > 0 && r1.value[0] !== "0.0.0.0") ? r1.value[0] : 
             ((r2 && r2.size > 0 && r2.value[0] !== "0.0.0.0") ? r2.value[0] : 
             ((r3 && r3.size > 0) ? r3.value[0] : "N/A"));
    
    return {writable: false, value: [ip, 'xsd:string']};

  lalu save 

🖋️ new > isi name contoh untuk redaman (RXPower) lalu masukan secrip
  
🖋️contoh perintah (secrip) untuk memunculkan keterangan RXPower / Redaman 

    const now = Date.now();
    
    let ProductClass = declare("DeviceID.ProductClass", {value: 1}).value[0];
    let signal = "N/A";
    
    switch (ProductClass) {
      case "F663NV3*":
        signal = declare("InternetGatewayDevice.WANDevice.*.X_CMCC_GponInterfaceConfig.RXPower",{value: 1}).value[0];
        break;
      default:
        let d = declare("InternetGatewayDevice.WANDevice.*.X_CMCC_GponInterfaceConfig.RXPower",{value: 1}).value[0];
        signal = Math.ceil(10 * Math.log10(d / 10000)).toString();
        break;
    }
    
    return {writable: false, value: [signal, 'xsd:string']};

  lalu save secrip nya 

🖋️ new > isi name contoh untuk nama modem (secreat_PPPoE) lalu masukan secrip

🖋️ contoh perintah (secrip) untuk memunculkan keterangan username / secreat_PPPoE

    const now = Date.now();
    
    let ProductClass = declare("DeviceID.ProductClass", {value: 1}).value[0];
    let pppoe_user = "N/A";
    
    if (/F663NV3*|F663NV9/i.test(ProductClass)) {
        let res = declare("InternetGatewayDevice.WANDevice.*.WANConnectionDevice.*.WANPPPConnection.*.Username", {value: 1});
    
        if (res && res.size > 0) { 
            pppoe_user = res.value[0];    }
    }
    
    return {writable: false, value: [pppoe_user, 'xsd:string']}; 

  lalu save secrip nya

🖋️ new > isi name contoh untuk waktu perangkat aktif (uptime) lalu masukan secrip

🖋️ contoh perintah (secrip) untuk memunculkan keterangan / 

    const now = Date.now();
    
    let r1 = declare("InternetGatewayDevice.DeviceInfo.UpTime", {value: 1});
    let r2 = declare("Device.DeviceInfo.UpTime", {value: 1});
    
    let s = (r1 && r1.size > 0) ? r1.value[0] : ((r2 && r2.size > 0) ? r2.value[0] : 0);
    if (!s) return {writable: false, value: ["N/A", 'xsd:string']};
    
    let d = Math.floor(s / 86400), h = Math.floor((s % 86400) / 3600), m = Math.floor((s % 3600) / 60);
    let hasil = (d > 0 ? d + "d " : "") + (h > 0 ? h + "h " : "") + m + "m";
    
    return {writable: false, value: [hasil, 'xsd:string']};

  lalu save secripnya

3. lalu kembali ke menu config >edit index page lalu edit bagian parameters

🖋️ pada v

  🖋️ pada label RXPower ubah menjadi VirtualParameters.rx_power
  
    - label: "'RXPower'"
      parameter: VirtualParameters.rx_power

  🖋️ pada label Uptime ubah menjadi VirtualParameters.uptime

     - label: "'Uptime'"
       parameter: VirtualParameters.uptime

  🖋️ pada label Secreat PPPoE ubah menjadi VirtualParameters.secreat_PPPoE

     - label: "'Secreat PPPoE'"
       parameter: VirtualParameters.secreat_PPPoE

  🖋️ pada label IP WAN/TR069 ubah menjaadi VirtualParameters.IPWAN_TR09

    - label: "'IP WAN/TR069'"
      parameter: VirtualParameters.IPWAN_TR09

4. selanjut nya masih pada menu admin ke Edit device page

  🖋️Agar modem kita dapat agar dapat memuculkan keterangan pada menu parameter, ke menu admin -> config ->edit device page
   
  🖋️cari teks seperti bawah ini, lalu pada bagian bawah tek tersebut tambahkan virtual parameters yang sudah di buat tadi

    - InternetGatewayDevice.DeviceInfo.HardwareVersion
    
    - InternetGatewayDevice.DeviceInfo.SoftwareVersion
    
    - InternetGatewayDevice.WANDevice..WANConnectionDevice..WANIPConnection.*.MACAddress
    
    - InternetGatewayDevice.WANDevice..WANConnectionDevice..WANIPConnection.*.ExternalIPAddress
    
    - InternetGatewayDevice.LANDevice..WLANConfiguration..SSID
    
    - InternetGatewayDevice.LANDevice..WLANConfiguration..KeyPassphrase
    
    - InternetGatewayDevice.LANDevice..Hosts.Host..HostName
    
    - InternetGatewayDevice.LANDevice..Hosts.Host..IPAddress
    
    - InternetGatewayDevice.LANDevice..Hosts.Host..MACAddress

  🖋️contoh teks yang di tambahkan 
  
   - VirtualParameters.rx_power
  - VirtualParameters.secreat_PPPoE
  - VirtualParameters.uptime
  - VirtualParameters.IPWAN_TR09
  
  secrip nya akan menjadi seperti ini

     - InternetGatewayDevice.DeviceInfo.HardwareVersion
     - InternetGatewayDevice.DeviceInfo.SoftwareVersion
     - InternetGatewayDevice.WANDevice..WANConnectionDevice..WANIPConnection.*.MACAddress
     - InternetGatewayDevice.WANDevice..WANConnectionDevice..WANIPConnection.*.ExternalIPAddress
     - InternetGatewayDevice.LANDevice..WLANConfiguration..SSID
     - InternetGatewayDevice.LANDevice..WLANConfiguration..KeyPassphrase
     - InternetGatewayDevice.LANDevice..Hosts.Host..HostName
     - InternetGatewayDevice.LANDevice..Hosts.Host..IPAddress
     - InternetGatewayDevice.LANDevice..Hosts.Host..MACAddress
     - VirtualParameters.rx_power
     - VirtualParameters.secreat_PPPoE
     - VirtualParameters.uptime
     - VirtualParameters.IPWAN_TR09
    
pastikan nama virtual parametersnya yang akan di tuliskan pastikan sama dengan saat tadi membuat parametersnya 

lalu coba sumon salah satu modem, pasti keterangandi parametersnya sudah mucul

tetapi jika ada salah 1 modem yang belum muncul keterangan parametrsnya 

ini tutor langkah langkahnya agar muncul 

    a. Show salah satu modem yang belum bisa muncul parameternya.
    
    b. Scroll keatas, akan muncul All parameters.
    
    c. Pada kolom pencarian ketik "InternetGatewayDevice.WANDevice" > enter.
    
    d. Bagian kanan ada tombol refreash, klik resfreash lalu klik commit. Tunggu sampai "committed"
    
    e. Scroll keatas, cari kata kunci di pencarian. Misal akan mencari secreat PPPoE berarti yang ditulis pada kolom pencarian yaitu "Username" > enter.
    
    f. Jika pada sebelah kanan belum muncul username modem tersebut, klik icon refreash > commit. Tunggu hingga commited.
    
    g. Setelah commited, kembali ke halaman devices awal, lihat modem yang sudah di summon dan di refreash tadi. Akan muncul Usernamenya.
    
5. selanjutnya cara agar summon nya bisa di sumon tanpa masuk ke menu modem
   
🖋️menambah secrp ke dalam cinfig > edit index page 

  - label: "'Action'"
  type: "'summon-button'"
  parameters:
    - InternetGatewayDevice.DeviceInfo.ModelName
    - InternetGatewayDevice.DeviceInfo.SoftwareVersion
    - InternetGatewayDevice.ManagementServer.ConnectionRequestURL
    - InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANIPConnection.1.ExternalIPAddress
