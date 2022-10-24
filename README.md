<p style="font-size:14px" align="right">
<a href="https://t.me/bangpateng_group" target="_blank">Join our telegram <img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/></a>
<a href="https://bangpateng.com/" target="_blank">Visit our website <img src="https://user-images.githubusercontent.com/38981255/184068977-2d456b1a-9b50-4b75-a0a7-4909a7c78991.png" width="30"/></a>
</p>

<p align="center">
  <img height="250" height="250" src="https://user-images.githubusercontent.com/38981255/197592560-3918c8df-c20b-4dd7-89f6-ea76a3f0f89d.png">
</p>

Dokumen Official :
> https://www.wormholes.com/docs/Install/index.html

## Perangkat Keras

|  Komponen |  Persyaratan Minimum |
| ------------ | ------------ |
| CPU  | Main frequency 2.9GHz, 4-core or above  |
| RAM | 8 GB  |
| Penyimpanan  | 500 GB HDD |

# WormholesChain Mirror Universe NO.2 Test Event SOP

## 1. Pastikan Kalian Sudah Memiliki VPS

### Install & Jalankan Node
```
sudo apt-get update && apt-get install wget
```
```
sudo apt-get install ca-certificates curl gnupg lsb-release -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```
```
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.6.1/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose
sudo chown $USER /var/run/docker.sock
```
```
docker pull wormholestech/wormholes:v1
```
```
docker run -d -p 30303:30303 -p 8545:8545 --name wormholes wormholestech/wormholes:v1
```

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/197593093-de2b889e-9aaf-42ec-914f-25308359f592.png">
</p>

### LALU JALANKAN
```
docker exec -it wormholes /usr/bin/cat /wm/.wormholes/wormholes/nodekey
```
Copy dan Import kunci pribadi 64-Bit Yang di Peroleh Saat Menjalankan Perintah di Atas dan Import ke WORMHOLES WALLET (Buat Wallet di : https://www.limino.com/#/wallet

## 2. Daftar Gleam Isi Data

https://gleam.io/1nbP9/mirror-universe-no2

- Join Discordnya : https://discord.gg/4Q5x8r4a
- Verification dan Klik Get Validator Role

-IP isi = Dengan IP VPS Kalian
-Get WormholesChain Address = Isi Dengan Address yg Sudah Kalian Import di https://www.limino.com/#/wallet
-Done

# 3. Kirim Email Ke Email Admin Untuk Mendapatkan Token Faucet 70.000 ERB Untuk Stake

Yang Pertama Jalankan Perintah di Bawah Ini Untuk Melihat Status Node, Paste Saja di Terminal dan Enter

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/197594295-41a5d0dd-ab41-4ccd-9499-71039b75c497.png">
</p>

```
#!/bin/bash
function info(){
     cn=0
     while true
     do
             echo "$cn second."
             echo "node $1"
             rs=`curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","id":64}' https://api.wormholestest.com 2>/dev/null`
             blockNumbers=$(parse_json $rs "result")
             echo "Block height of the whole network: $((16#${blockNumbers:2}))"
             rs1=`curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"net_peerCount","id":64}' 127.0.0.1:$1 2>/dev/null`
             count=$(parse_json $rs1 "result")
             echo "Number of node connections: $((16#${count:2}))"
             rs2=`curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_blockNumber","id":64}' 127.0.0.1:$1 2>/dev/null`
             blckNumber=$(parse_json $rs2 "result")
             echo "Block height of the current peer: $((16#${blckNumber:2}))"
             sleep 5
             clear
             let cn+=5
     done
}

function parse_json(){
      if [[ $# -gt 1 ]] && [[ $1 =~ $2 ]];then
         echo "${1//\"/}"|sed "s/.*$2:\([^,}]*\).*/\1/"
      else
         echo "0x0"
     fi
}

function main(){
     if [[ $# -eq 0 ]];then
             info 8545
     else
             info $1
     fi
}

main "$@"
```
Nanti Akan Muncul Tampilan Seperti di Bawah ini, Jangan Lupa Untuk di Screenshoot (Kita Membutuhkan Untuk Kirim Email ke Admin)

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/197594574-484b47a4-e661-48ee-9d4b-339157d632a9.png">
</p>

### Send Email

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/197600515-c8d61ff3-e148-405b-aa03-590a37bdf402.png">
</p>


Kirimkan Screenshoot nya dan Kirimkan Address Wormholes nya Kirim ke Email *market@wormholes.com*

*SELESAI.. UNTUK LANJUTAN TUNGGU DAPAT EMAIL.. PANTAU DI CHANNEL https://t.me/bangpateng_airdrop*
