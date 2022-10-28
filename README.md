<p style="font-size:14px" align="right">
<a href="https://t.me/bangpateng_group" target="_blank">Join our telegram <img src="https://user-images.githubusercontent.com/50621007/183283867-56b4d69f-bc6e-4939-b00a-72aa019d1aea.png" width="30"/></a>
<a href="https://bangpateng.com/" target="_blank">Visit our website <img src="https://user-images.githubusercontent.com/38981255/184068977-2d456b1a-9b50-4b75-a0a7-4909a7c78991.png" width="30"/></a>
</p>

<p align="center">
  <img height="250" height="250" src="https://user-images.githubusercontent.com/38981255/197592560-3918c8df-c20b-4dd7-89f6-ea76a3f0f89d.png">
</p>

Dokumen Official :
> https://www.wormholes.com/docs/Install/index.html

Detail Event :
> https://medium.com/wormholeschain-network/mirror-universe-no-2-e644c69e4e84

## Perangkat Keras

|  Komponen |  Persyaratan Minimum |
| ------------ | ------------ |
| CPU  | Main frequency 2.9GHz, 4-core or above  |
| RAM | 8 GB  |
| Penyimpanan  | 500 GB HDD |

# WormholesChain Mirror Universe NO.2 Test Event SOP

### Install Docker

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/198647832-190633a4-01b9-4bd3-9c03-9c90e7a00915.png">
</p>

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

## Buat Bash

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/198648134-11bb6769-5dd5-41e4-abf0-bf6e1618d950.png">
</p>

```
nano wormholes_install.sh
```

Masukan Dengan Script di Bawah Ini :

```
#!/bin/bash
#check docker cmd
which docker >/dev/null 2>&1
if  [ $? -ne 0 ] ; then
     echo "docker not found, please install first!"
     echo "ubuntu:sudo apt install docker.io -y"
     echo "centos:yum install  -y docker-ce "
     echo "fedora:sudo dnf  install -y docker-ce"
     exit
fi
#check docker service
docker ps > /dev/null 2>&1
if [ $? -ne 0 ] ; then

     echo "docker service is not running! you can use command start it:"
     echo "sudo service docker start"
     exit
fi

docker stop wormholes > /dev/null 2>&1
docker rm wormholes > /dev/null 2>&1
docker rmi wormholestech/wormholes:v1 > /dev/null 2>&1

if [ -d /wm/.wormholes/keystore ]; then
   read -p "Whether to clear the Wormholes blockchain data history, if yes, press the “y” button, and if not, click “enter.”：" xyz
   if [ "$xyz" = 'y' ]; then
         cp /wm/.wormholes/wormholes/nodekey /wm/nodekey
         rm -rf /wm/.wormholes
         mkdir -p /wm/.wormholes/wormholes
         mv /wm/nodekey /wm/.wormholes/wormholes/
   else
         echo "Do not clear"
   fi
else
   read -p "Please import your private key：" ky
fi

if [ -n "$ky" ]; then
     if [ ${#ky} -eq 64 ];then
             mkdir -p /wm/.wormholes/wormholes
             echo $ky > /wm/.wormholes/wormholes/nodekey
     elif [ ${#ky} -eq 66 ] && ([ ${ky:0:2} == "0x" ] || [ ${ky:0:2} == "0X" ]);then
             mkdir -p /wm/.wormholes/wormholes
             echo ${ky:2:64} > /wm/.wormholes/wormholes/nodekey
     else
             echo "the nodekey format is not correct"
             exit -1
     fi
fi

docker run -id -p 30303:30303 -p 8545:8545 -v /wm/.wormholes:/wm/.wormholes --name wormholes wormholestech/wormholes:v1

echo "Your private key is:"
sleep 6
docker exec -it wormholes /usr/bin/cat /wm/.wormholes/wormholes/nodekey
```

## Eksekusi Bash Script nya

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/198648457-c5bb09fd-3418-4e75-a3e9-c9e2947ff134.png">
</p>

```
bash ./wormholes_install.sh
```
- Masukan Private Key Yang Sebelumnya Sudah Kalian Miliki Ambil di Website : https://www.limino.com/#/wallet
- Setingan > Security Dan Privacy
- Masukan Katasandi Kalian
- Ambil Private Key nya
- Paste ke Terminal VPS nya
- Enter dan Biarkan Docker Running

## Check Status Node

```
curl -X POST -H 'Content-Type:application/json' --data '{"jsonrpc":"2.0","method":"net_peerCount","id":1}' http://127.0.0.1:8545
```
Dan Jalankan Perintah di Bawah Langsung paste Saja di Terminal VPS Kalian

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

Anda Akan Melihat Seperti Gambar di Bawah ini :

<p align="center">
  <img height="auto" height="auto" src="https://user-images.githubusercontent.com/38981255/198654914-6cb8b0ed-08db-4ab0-b377-ab220d636572.png">
</p>

TUTOR MINER TUNGGU FAUCET Di BAGIIN 

Aset uji akan memulai proses pelepasan ketika ketinggian blok mencapai 140000. Setelah menyelesaikan distribusi aset uji,

kami akan mengirimkan email konfirmasi dan email yang berisi proses penyiapan lengkap. Harap jaga agar kotak surat Anda tetap terbuka selama acara.
