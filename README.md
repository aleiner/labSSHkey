# Install RKE2

On All Nodes:

```bash
cat >> /etc/NetworkManager/conf.d/rke2-canal.conf << EOF
[keyfile]
unmanaged-devices=interface-name:cali*;interface-name:flannel*
EOF

systemctl reload NetworkManager
```

On First Node:

```bash
curl -sfL https://get.rke2.io | sh -
systemctl enable rke2-server.service 
systemctl start rke2-server.service
```

On First Node:

```bash
cat >> ~/.bashrc <<EOF
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml
export PATH=$PATH:/var/lib/rancher/rke2/bin:/usr/local/bin
export CRI_CONFIG_FILE=/var/lib/rancher/rke2/agent/etc/crictl.yaml
#export KU_NS=default
#alias ku="kubectl -n \\\$KU_NS"
alias ku="kubectl"
alias k="kubectl"
EOF
source ~/.bashrc

```

On First Node:
```
dnf install -y https://github.com/derailed/k9s/releases/download/v0.50.18/k9s_linux_amd64.rpm
```

On First Node:

```
cat /var/lib/rancher/rke2/server/node-token
```

On Second and Third Node:

```
curl -sfL https://get.rke2.io | sh -
systemctl enable rke2-server.service 
```

On Second and Third Node:
```bash
cat >> /etc/rancher/rke2/config.yaml << EOF
server: https://10.7.2.12:9345
token: K104d27666dcebe13f6994516a9fee04731669182a95a44862afa11a8bd8021208e::server:f40634780a58ac1477c972806abec087
EOF
```