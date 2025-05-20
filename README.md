# Basit-anlatim-Aztec-Sequence-Node-kurulumu
Aztec Network Testnet'te `Sequencer Node`'un nasıl çalıştırılacağına ve `Apprentice` Rolünün nasıl kazanılacağına dair adım adım bir kılavuz.

* **Testnet'e hangi düğüm türleri katılabilir?**
  * `Sequencer`: blokları önerir, diğerlerinden gelen blokları doğrular ve yükseltmeler için oylama yapar.
 * `Prover`: toplama bütünlüğünü doğrulayan ZK kanıtları üretir.

## Rol Bilgileri
Sequecner Düğümleri, Discord'daki katkıları için belirli bir rol alacaklar.

Sequencer düğümünüzü çalıştırıp senkronize ettikten sonra [Rol Al](https://github.com/0xmoei/aztec-network/blob/main/README.md#get-apprentice-discord-role) adımını uygulayabilirsiniz.

---

## Donanım Gereksinimleri (Minimum)
<table>
<tr>
<th colspan="3"> Aztec Sequence Node için Donanım Gereksinimleri </th>
</tr>
<tr>
<td>RAM</td>
<td>CPU</td>
<td>Disk</td>
</tr>
<tr>
<td><code>8-16 GB</code></td>
<td><code>4-9 çekirdek</code></td>
<td><code>100+ GB SSD</code></td>
</tr>
</table>

* **Prover Düğümü**: 16 çekirdek ve 128 GB RAM'e sahip ~40x makine gerektirir
* `Prover`'ı çalıştırmıyorum çünkü bu benim için değil, veri merkezi bilgi işlem sistemleri için. Bu bilgiyi bende bilmiyordum. Neyse öğrenmiş olduk.

---


**VPS Kullanıcıları**: 4 çekirdekli CPU ve 8 GB RAM'e sahip bir `VPS` ile başlayabilir! Ancak uzun süreli çalıştırmayı düşünüyorsanız 1tb ssd li Kaliteli ve ucuz bir vps almanızı tavsiye ederim. [Buradan satın alın](https://www.netcup.com/en/server/vps)
* ![VPS 4000 G11](https://github.com/user-attachments/assets/1088fd9c-9607-46e1-a489-8b9012b3242f)
* Aşağıda sizlere indirimden faydalanabileceğiniz ve ilk ay ücretsiz kullanabileceğiniz 25 tane farklı kod bırakıyorum.
* Unutmayın her bir kod sadece bir kere kullanılabilir. Tavsiye ettiğim sistem (VPS 4000 G11) sistemidir
*KODLAR: 4103nc174776235424 --- 4103nc174776235423 --- 4103nc174776235422 --- 4103nc174776235421 --- 4103nc174776235420 --- 4103nc174776235419 --- 4103nc174776235418 --- 4103nc174776235417 --- 4103nc174776235416 --- 4103nc174776235415 --- 4103nc174776235414 --- 4103nc174776235413 --- 4103nc174776235412 --- 4103nc174776235411 --- 4103nc174776235410 --- 4103nc17477623549 --- 4103nc17477623548 --- 4103nc17477623547 --- 4103nc17477623546 --- 4103nc17477623545 --- 4103nc17477623544 --- 4103nc17477623543 --- 4103nc17477623542 --- 4103nc17477623541 --- 4103nc17477623540

---

## Sunucuyu satın aldıktan sonra Ip adresinizi ve Sunucu için aldığınız şifreyi kaydedin. SUNUCUNUZA GİRİŞ YAPIN

## 1. Güncellemeleri Yükleyin
* Update packages:
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

* Paketleri Kurun:
```bash
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```

* Docker'ı yükleyin:
```bash
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world

sudo systemctl enable docker
sudo systemctl restart docker
```

---

## 2. Aztec Tools'u yükleyin
```bash
bash -i <(curl -s https://install.aztec.network)
```
```bash
echo 'export PATH="$HOME/.aztec/bin:$PATH"' >> ~/.bashrc

source ~/.bashrc
```
* **Terminalinizi yeniden başlatın** sudo reboot yazın Ya da 
* iki kere exit exit yazarak da veya (direk terminali çarpı işaretinden de kapatabilirsiniz sorun olmaz arka planda dosyalar yüklü ve henüz screen kurmadık)
* Kurulumun başarılı olup olmadığını kontrol edin:
```bash
aztec
```

---

## 3. Aztec'i güncelleyin
```bash
aztec-up alpha-testnet
```

---

## 4. RPC URL'lerini edinin
* Sepolia `RPC URL` ve Sepolia `BEACON URL` API'lerini destekleyen bir 3. taraf bulun. (ücretsiz olanlar size apprentice rolü verir ama guardian için yeterli olmaz)
* Kullanımınızın çoğu `RPC URL`dir. `RPC URL` ve `Beacon URL` için [Chainstack](https://chainstack.com/) adresine gidip ücretli rpc kullanmanızı kullanmanızı öneririm. Kendi RPC'nizi kurmak istiyorsanız farklı rehberlerden yararlanabilirsiniz.

**RPC çözümleri hakkında daha fazla bilgi**:

### Geth ve Prysm Düğümlerini Çalıştırarak Kendi RPC'nizi Edinin
* Bu kılavuzu izleyerek kendi yerel RPC düğümlerinizi çalıştırabilirsiniz: [geth-prysm-node](https://github.com/ultramit1/geth-prysm-node) 600-1000 GB SSD'ye ihtiyacınız olabilir

### Ücretsiz RPC'ler: 
* `RPC URL`: Sepolia Ethereum HTTP API'sini oluşturun [Alchemy](https://dashboard.alchemy.com/)
* `BEACON RPC`: Bir hesap oluşturun [drpc](https://drpc.org/) ve şurayı bulun `Sepolia Ethereum Beacon Chain ` Endpoints.

![Örnek Resim](https://github.com/user-attachments/assets/cea54713-bb28-4d7d-90cf-dca47c47e9ee)

### Paralı RPC: 
[Chainstack](https://chainstack.com/)

Yukardaki Chainstack linkine gidin: Orada aylık abonelik açabilirsiniz. Ayda 50$ ile bir ay sorunsuz çalıştırabilirsiniz. 20 milyon request hakkınız var yeterli olacağını düşünüyorum.
![Image](https://github.com/user-attachments/assets/bf9964e9-24c1-4194-961b-b2d42a9320ba)

---


> Tekrardan hatırlatma Kendi `RPC URL` ve `BEACON RPC`'nizi elde etmek için kendi Geth ve Prysm düğümlerinizi çalıştırabilir veya diğer 3. parti çözümleri bulabilirsiniz. [geth-prysm-node](https://github.com/ultramit1/geth-prysm-node)

---

## 5. Yeni bir Ethereum Cüzdanı oluşturun. Sadece testnet için kullanın ve içine sepolia test etherum atın.
`Özel Anahtar` ve `Cüzdan Adresinizi` kaybetmemek için bir yere not alın veya bilgisayarınızdaki bir klasöre yedekleyin.(Hızlı bir şekilde ordan kopyalayıp sunucu içine yazmak için)

---

## 6. Cüzdanınıza Nasıl Sepolia ETH edinilir?
[Alchemy faucet](https://www.alchemy.com/faucets/ethereum-sepolia) veya ![GPU ile kazım yaparak da alabilirsiniz. En az 10dk çalışması lazım] [POW faucet](https://sepolia-faucet.pk910.de)

---

## 7. IP'nizi bulun ve kaydedin. Satın aldığınız sunucunun Ip'sini kayıt edin bunları rol almak için kullanacaksınız. 
```bash
curl ipv4.icanhazip.com
```
* Sunucuya bu kodu girdikten sonra çıkan sonucu Kaydedin

---

## 8. Güvenlik Duvarını Etkinleştirmek güvenlik için önemlidir. Bunu yapın ve Bağlantı Noktalarını Açın
```console
# Firewall
ufw allow 22
ufw allow ssh
ufw enable

# Sequencer
ufw allow 40400
ufw allow 8080
```

---

## 9. Sequencer Node'u Çalıştırın
Sequencer Node'u şu iki yöntemden biriyle çalıştırabilirsiniz: `Docker` veya `CLI` Biz bu rehberde CLI olarak çalıştıracağız. Docker kurup sorun yaşayanlara rastladığım için screen ile kurmayı tercih ettim.

* Screen Kurun
```bash
screen -S aztec
```
* Bu kod yeni bir screen açacaktır. Bundan sonra yapacaklarımız bu ekranda kayıtlı olacak. Ne olursa olsun işiniz bittikten sonra muhakkak ------->Ctrl+a ve D'ye <--------- basıp çıkın.

* Node'u başlatmak için aşağıdaki kodları bir not defterine kopyalayıp belirtilen yerleri kendi bilgilerinizle değiştirin:
* Cüzdan gizli anahtarını başına 0x koyarak yazınız örnek cüzdanın 111 ile başlıyorsa başına 0x gelecek yani 0x111 olacak.
* Cüzdan public adresinizin başına ekstra 0x koymanıza gerek yok. Ben 0x koymadan olduğu gibi yaptım oldu. Bazılarında problem çıkmış önce koymadan deneyin olmazsa koyarsınız.
* Execution ve Beacon rpc'lerini kopyala ve oraya yapıştır.
* En son IPburaya olan yeri silin ve oraya IP'nizi yaazın.

Node'u çalıştırmadan önce aşağıdaki değişkenleri değiştirin:
* `RPC_URL` & `BEACON_URL`: Satın aldığınız veya Kendi Kurduğunuz Rpc'nin bilgilerini girin.
* `0xÖzelanahtarın`: `0x...` başa koyup EVM cüzdan özel anahtarınızı girin.
* `0xCüzdanadresin`:  EVM cüzdan public adresiniz.
* `IPBURAYA`: Sunucu IP'nizi girin.

  
```
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls RPC_URL  \
  --l1-consensus-host-urls BEACON_URL \
  --sequencer.validatorPrivateKey 0xÖzelanahtarın \
  --sequencer.coinbase 0xCüzdanadresin \
  --p2p.p2pIp IPBURAYA
  --p2p.maxTxPoolSize 1000000000
```

---

* BU KODU GİRDİKTEN SONRA NODE ÇALIŞMAYA VE SENKRONİZE OLMAYA BAŞLAYACAKTIR. EKRANI CTRL+ A + D ile kapatabilirsiniz.
* Bu sizi sunucunuzun giriş sekmesine atacaktır. Şimdi logların biraz akmasını ve blockların senkronize olmasını yani son bloğa gelmesini bekliyeceğiz İşlem birazcık sürebilir. Bu sırada aşağıdaki komutları girebilirsiniz:

---

**Adım 1: En son kanıtlanmış blok numarasını alın:**
```bash
curl -s -X POST -H 'Content-Type: application/json' \
-d '{"jsonrpc":"2.0","method":"node_getL2Tips","params":[],"id":67}' \
http://localhost:8080 | jq -r ".result.proven.number"
```
* Bu blok numarasını sonraki adımlar için kaydedin
* Örnek çıktı: 80214 ( size farklı bir rakam verir)

**Adım 2: Eşitleme kanıtınızı oluşturun**
```bash
PROVEN_BLOCK=$(curl -s -X POST -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","method":"node_getL2Tips","params":[],"id":67}' \
  http://localhost:8080)
CURL_EXIT_CODE=$?

if [[ "$CURL_EXIT_CODE" -ne 0 ]]; then
  echo "Error: Failed to connect to the aztec nodes HTTP API on port 8080."
  echo "Pls ensure your aztec node is running and its HTTP API is listening on http://localhost:8080."
  if [[ "$CURL_EXIT_CODE" -eq 7 ]]; then
    echo "Common error: Connection refused. This usually means no process is listening on that port."
  else
    echo "Curl error code: $CURL_EXIT_CODE"
  fi
else
  PROVEN_BLOCK=$(echo "$PROVEN_BLOCK" | jq -r ".result.proven.number")

  if [[ -z "$PROVEN_BLOCK" || "$PROVEN_BLOCK" == "null" ]]; then
    echo "Failed to retrieve the proven L2 block number from the API response."
  else
    echo "Proven L2 Block Number: $PROVEN_BLOCK"
    echo "Fetching Sync Proof..."
    SYNC_PROOF=$(curl -s -X POST -H 'Content-Type: application/json' \
      -d "{\"jsonrpc\":\"2.0\",\"method\":\"node_getArchiveSiblingPath\",\"params\":[\"$PROVEN_BLOCK\",\"$PROVEN_BLOCK\"],\"id\":68}" \
      http://localhost:8080 | jq -r ".result")

    echo "Sync Proof:"
    echo "$SYNC_PROOF"
  fi
fi
```
* Proof alma kodunu yazdıktan sonra size AAAAAAAile başlayan uzun tuhaf bir kod verir onun tümünü kaydedin discordda onu girip rol alacaksınız.

---

## Apprentice Discord Rolünü Alın:
Discord kanalına gidin: ![örnek resim](https://github.com/user-attachments/assets/98523f9f-1613-4ef5-a287-e43a7dfcef8e)

---

**SON ADIMLAR: Discord'a kaydolun**
* Herşey senkronize olup node sorunsuz çalıştıktan sonra Bu Discord sunucusunda şu komutu yazın: `/operator start`
* Komutu yazdıktan sonra, Discord şuna benzeyen seçenek alanlarını görüntüler:
* `address`: Doğrulayıcı adresiniz (Ethereum Adresi)
* `block-number`: Doğrulama için blok numarası (aldığınız blok numarası)
* `proof`: Senkronizasyon kanıtınız (AAAAA ile başlayan uzun base64 dizesi)

Ardından `Apprentice` Rolünüzü alacaksınız

![Resim](https://github.com/user-attachments/assets/8cb44940-bf62-4a69-a051-c7d2bf5359fc)

## SON OLARAK GUARDİAN OLMAK İÇNİ ACELE ETMEYİN EN AZ 2 GÜN ÇALIŞTIRIN. Apprentice rolü aldıktan sonra #upgrade role kanalından guardian olmak için /IP sekmesinden Ip adresinizi aratarak rol yükseltebilirsiniz. Kolay gelsin.

---

## 🔃 Sequencer Node'u Güncelle ( Olurda AZTEC GÜNCELLEME DUYURURSA TEKRARDAN HERŞEYİ BAŞA ALMANA GEREK YOK)
* 1- Düğümü Durdur:
```console
# CLI
docker stop $(docker ps -q --filter "ancestor=aztecprotocol/aztec") && docker rm $(docker ps -a -q --filter "ancestor=aztecprotocol/aztec")

screen -ls | grep -i aztec | awk '{print $1}' | xargs -I {} screen -X -S {} quit
```

* 2- Node'u Güncelle:
```bash
aztec-up alpha-testnet
```

* 3- Eski verileri sil:
```bash
rm -rf ~/.aztec/alpha-testnet/data/
```

* 4- Düğümü yeniden çalıştırın (AŞAĞIDAKİ BİLGİLERİ YİNE KENDİNİZE GÖRE AYARLAYIN VE BAŞLATIN)
```
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls RPC_URL  \
  --l1-consensus-host-urls BEACON_URL \
  --sequencer.validatorPrivateKey 0xÖzelanahtarın \
  --sequencer.coinbase 0xCüzdanadresin \
  --p2p.p2pIp IPBURAYA
  --p2p.maxTxPoolSize 1000000000
```

---

### İsteğe Bağlı Komutlar:
**Ekran Komutları:**
* Ekranı küçült Yani ekranı arka planda çalışır bir şekilde kapatmak: `Ctrl` + `A` + `D`
* Ekrana geri dön: `screen -r aztec`
* Ekranı sonlandır (içerideyken. Ama şimdi yapmayın sakın): `Ctrl`+`C+
* Ekranı sonlandır (dışarıdayken): `screen -XS aztec quit`

SAYGILAR SEVGİLER
