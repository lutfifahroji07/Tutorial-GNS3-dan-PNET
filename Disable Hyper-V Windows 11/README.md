
# Cara Disable Hyper-V di Windows 11 Works

Ini saya buat karena saya kesal, sangat sulit sekali mendisable hyper-v, saya ingin menginstal gns3 vm/pnet lab pada vm ware, tapi selau ada popup "Virtualized Intel-VT-x/EPT Is Not Supported on This Platform", dan caranya membenarkannya adalah dengan menonaktifkan hyper-v dan mengaktfikan virtualisasi pada bios, tapi disini saya hanya kasih tutor untuk menonaktifkan hyper-v sampe akar2nya...btw saya sampe install ulang windows hanya karna Ini....

## CARA KE1
#### Dari Control Panel

Klik Start ➡️ Cari Turn Windows features on or off ➡️ Unchecklist Hyper-V dan Virtual Machine Platform ➡️ Klik OK dan Restart

Berikut Screenshot caranya:

</p>1️⃣<img src="/screenshot/ss1.png" style="width: 50%; height: 50%;">

</p>2️⃣<img src="/screenshot/ss2.png" style="width: 50%; height: 50;">

##### NOTE: kalo masih gag bisa lanjut ke cara ke2 dan seterusnya...


## CARA KE2
#### Dengan CMD

Buka CMD jalankan dengan run as administrator ➡️ Ketik Command ini ⬇️ dan Restart
```bash
bcdedit /set hypervisorlaunchtype off
```
Berikut Screenshot caranya:

</p>1️⃣<img src="/screenshot/ss3.png" style="width: 50%; height: 50%;">

</p>2️⃣<img src="/screenshot/ss4.png" style="width: 50%; height: 50%;">


## CARA KE3
#### Dengan PowerShell

Buka PowerShell jalankan dengan run as administrator ➡️ Ketik Command ini ⬇️ dan Restart
```bash
Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-Hypervisor
```
Berikut Screenshot caranya:

</p>1️⃣<img src="/screenshot/ss5.png" style="width: 50%; height: 50%;">

</p>2️⃣<img src="/screenshot/ss6.png" style="width: 50%; height: 50%;">

`
`

<br>

Jika setelah Restart masih tidak bisa coba lagi dengan command ini dan kemudian Restart lagi...
```bash
dism /online /disable-feature /featurename:microsoft-hyper-v-all
```
Berikut Screenshot caranya:

1️⃣![SS7](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

<br>

Kalo masih gag bisa juga coba command ini dan Restart lagi... kalo masih gag bisa juga lanjut Cara ke4...
```bash
get-netadapter|where-object {$_.interfacedescription -like "*hyper-v*"}|Disable-NetAdapter
```
Berikut Screenshot caranya:

1️⃣![SS8](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

<br>

## CARA KE4
#### Dengan Edit Registry Editor/Regedit

Ini adalah cara yang paling ampuh disaya, setelah melakukan cara ini akhirnya hyper-v saya berhasil di disable...

1️⃣ Klik kanan tombol Start dan pilih Run.

2️⃣ Ketik regedit dan tekan Enter.
![SS9](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

3️⃣ Pada Search Bar cari ini dan tekan Enter.
```bash
Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceGuard
```

4️⃣ Klik kanan pada layar, Klik new ➡️ DWORD (32-bit) Value dan beri nama EnableVirtualizationBasedSecurity .

5️⃣ Klik dua kali pada Nilai DWORD baru yang Anda buat, atur data nilainya ke 0, dan klik tombol OK.
![SS10](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

6️⃣ Selanjutnya klik Search Bar lagi cari ini dan tekan Enter.
```bash
Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa
```
7️⃣ Buat Nilai DWORD baru dan beri nama LsaCfgFlags .

8️⃣ Anda dapat menonaktifkan Credential Guard dengan menetapkan nilai LsaCfgFlags ke 0.
![SS11](https://via.placeholder.com/468x300?text=App+Screenshot+Here)

9️⃣ Trakhir klik Search Bar lagi cari ini dan tekan Enter.
```bash
Komputer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceGuard\Skenario\HypervisorEnforcedCodeIntegrity
```
🔟 Ubah value data dari Enabled DWORD dari 1 menjadi 0 untuk disable memory isolation.
![SS12](https://via.placeholder.com/468x300?text=App+Screenshot+Here)
