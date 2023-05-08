#Installation Steps
##Step 1: Disable Swap
Run the following command to disable swap:

```bash
```sh
$ sudo swapoff -a

### Step 2: Update /etc/fstab
```bash
```sh
$ sudo sed -i '/\sswap\s/s/^/#/' /etc/fstab


### Step 3: Update /etc/hosts
```bash
```sh
$ sudo sed -i '/<IP_address>/d; $a\<IP_address>\t<hostname>' /etc/hosts


### Step 4: Enable Bridged Traffic in IPTABLES
```bash
```sh
$ echo -e "overlay\nbr_netfilter" | sudo tee /etc/modules-load.d/containerd.conf >/dev/null && cat /etc/modules-load.d/containerd.conf
$ sudo modprobe overlay
$ sudo modprobe br_netfilter
$ echo -e "net.bridge.bridge-nf-call-iptables  = 1\nnet.bridge.bridge-nf-call-ip6tables = 1\nnet.ipv4.ip_forward                 = 1" | sudo tee /etc/sysctl.d/k8s.conf >/dev/null && cat /etc/sysctl.d/k8s.conf



### Step 5: Install Container Runtime (containerd)
```bash
```sh
$ wget https://github.com/containerd/containerd/releases/download/v1.6.16/containerd-1.6.16-linux-amd64.tar.gz -P /tmp/
$ tar Cxzvf /usr/local /tmp/containerd-1.6.16-linux-amd64.tar.gz
$ wget https://raw.githubusercontent.com/containerd/containerd/main/containerd.service -P /etc/systemd/system/
$ systemctl daemon-reload
$ systemctl enable --now containerd



