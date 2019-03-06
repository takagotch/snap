### snap
---
https://github.com/intelsdi-x/snap

```
```

```
go get -u github.com/go-swagger/go-swagger/cmd/swagger

echo "" | sudo tee -a /etc/apt/source/
sudo apt-get update
sudo apt-get install swagger

curl -LO https://github.com/go-swagger/go-swagger/releases/download/0.10.0/swagger_linux_amd64
chmod +x swagger_linux_amd64 && sudo mv swagger_linux_amd64 /usr/bin/swagger

curl -s https://packagecloud.io/install/repositories/intelsdi-x/snap/script.rpm.sh | sudo bash
sudo yum install -y snap-telemetry

curl -s https://packagecloud.io/install/repositories/intelsdi-x/snap/script.deb.sh | sudo bash
sudo apt-get install -y snap-telemetry

curl -s https://packagecloud.io/install/repositories/intelsdi-x/snap/script.deb.sh | sudo os=ubuntu dist=trusty bash
sudo apt-get install -y snap-telemetry

brew install snap-telemetry
curl -sfL mac.pkg.dl.snap-telemetry.io -o snap-telemetry.pkg
sudo installer -pkg ./snap-telemetry.pkg -target /

curl -sfL linux.tar.dl.snap-telemetry.io -o snap-telemetry.tar.gz
tar xf snap-telemetry.tar.gz
cp cnapteld /usr/local/sbin
cp snaptel /usr/local/bin

snapctl

service snap-telemetry start

systemctl start snap-telemetry

sudo mkdir -p /var/log/snap
sudo snapteld --plugin-trust 0 --log-level 1 --log-path /var/log/snap &

tail -f /var/log/snap/snapteld.log

export OS=$(uname -s | tr '[:upper:]' '[:lower:]')
export ARCH=$(uname -m)
curl -sfL "https://github.com/intelsdi-x/snap-plugin-publisher-file/releases/download/2/snap-plugin-publisher-file_${OS}_${ARCH}" -o snap-plugin-publisher-file
curl -sfL "https://github.com/intelsdi-x/snap-plugin-collector-psutil/releases/download/8/snap-plugin-collector-psutil_${OS}_${ARCH}" -o snap-plugin-collector-psutil

snaptel plugin load snap-plugin-publisher-file
snaptel plugin load snap-plugin-collector-psutil
snaptel plugin list

snaptel metric list
curl https://raw.githubusercontent.com/intelsdi-x/snap/master/examples/tasks/psutil-file.yaml -o /tmp/psutil-file.yaml
snaptel task create -t /tmp/psutil-file.yaml

tail -f /tmp/psutil_metrics.log
snaptel task watch 8b9babad-b3bc-4a16-9e06-1f35664a7679
```

```
```


