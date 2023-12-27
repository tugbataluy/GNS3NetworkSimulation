# GNS3NetworkSimulation
GNS3 kullanarak bir merkez ve bir dal ofisten oluşan şirketin ağ simülasyonu

## İzlenilen Adımlar
1. GNS3 yazılımını ve sanal makinesini indirin.
  * https://gns3.com/software/download-vm
  * https://gns3.com/software/download
2. GNS3 sanal makinesini Hyper-V kullanarak oluşturun.
  * https://www.youtube.com/watch?v=2E8bcnooTiY&t=715s
  * Eğer buradaki adımları kullanarak çalıştıramazsanız hypervGns3(ShellScriptKomutları).txt adlı dosyaya göz atın.
3. Ağınızı oluşturmadan önce bir planını çıkarın (Örnek Excel dosyası mevcuttur.).
4. Gerekli cihazları "Add New Template" den ekleyin. Kendi ISO dosyalarınızla ya da Gns3 nin sağladığı ISO dosyalarını kullanarak bu işlemi tamamlayabilirsiniz.
  * https://www.youtube.com/watch?v=sLyyS4lUeEI
5. İstediğiniz sırayla cihazlarınızı konfigüre edin.

## Projedeki Tasarımım
Merkez ve dal olmak üzere 2 farklı kolum mevcut. Bunların her ikisinde de switchleri spine leaf ağ topolojisini kullanarak yerleştirdim. Hem leaf hem spine switchlere ait bağlantılar arasında LAG (Link Aggregation) yapılanması ve MLAG (Multi-Chassis Link Aggregation kullandım). Merkez kolunda firewall clusterımı OpenSUSE kullanarak oluşturdum. Bu sayede terminal üzerinden ve Yast2 arayüzü ile firewall yapılandırmasını deneyimleme imkanım oldu. Merkezde strongswanden faydalanarak IPsec konfigürasyonumu yaptım ve ipsec dosyalarımı kendim yazdım. Ayrıca 2 firewallın yedekli çalışmasını keepalived kullanarak (VRRP Protokolüyle sağladım).

Dalda ise firewalları pfSense seçtim ve görsel bir arayüz kullanarak firewallu nasıl yapılandıracağımı da deneyimlemiş oldum. Burada yedekliliği CARP protokolünü kullanarak sağladım. VPN için de OpenVPN i kullandım.
Uç cihazlarımda docker üzerinden yapılanmış linuz cihazları kullandım. Bu yüzden session sonunda içlerindeki bilgileri kaybetmemek için dışarıdan dizin belirterek session bilgilerini kaydettim.

## Ağ Tasarımım


![AğTopolojisi](https://github.com/tugbataluy/GNS3NetworkSimulation/assets/76051144/79ed4ee5-e1c0-486e-ad62-05c455528cca)

## Docker Konteyberlarına Eklediğim Harici Dizinler
![image](https://github.com/tugbataluy/GNS3NetworkSimulation/assets/76051144/529ef08b-667c-4429-b5c1-6e85881d03e3)

