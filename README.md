# Testing api-v4 change in api-dev

* Create branch with changes
* Run GitHub action to create docker image
* Update `values-dev.yaml` with new tag.
* Run `helm upgrade api-dev ./chart -f values-dev.yaml`. Refer to [this](https://github.com/traveltime-dev/traveltime-platform/blob/871ed289603edbb123c28684b1965f20b4573a16/.kube/helm/api-v4/README.md) if needed.

New changes should be live in https://api-dev.traveltimeapp.com

# Slow internet speed on RTL8111/8168/8411

```bash
sudo apt update
sudo apt install r8168-dkms

sudo reboot

lsmod | grep r8168
```

If `lsmod | grep r8168` is empty, you might have to disable secure boot in BIOS (bios key - F1) and then load it manually (look further)

```bash
dkms status
```

If this is not empty, then driver was installed, but not loaded.

We can load it manually

```bash
sudo modprobe -r r8169
sudo modprobe r8168
```

If this works (and internet speed went up) we can make it permanent

```bash
sudo nano /etc/modprobe.d/r8168.conf
```
Paste `blacklist r8169`
