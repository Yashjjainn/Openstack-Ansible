# Openstack-Ansible

This guide helps you install OpenStack using the official **OpenStack-Ansible** AIO setup on Ubuntu.

---

## ✅ Step 1: Update All Packages

Update your system and reboot:

```bash
sudo apt update
sudo apt dist-upgrade
reboot
```

---

## ✅ Step 2: Install SSH, Git, and Pip

Install required dependencies:

```bash
sudo apt update
sudo apt install -y openssh-server
sudo apt install -y git
sudo apt install -y python3-pip
```

---

## ✅ Step 3: Clone OpenStack-Ansible Repository

Switch to root and clone the official repo:

```bash
sudo -i

# Clone OpenStack-Ansible
git clone https://opendev.org/openstack/openstack-ansible /opt/openstack-ansible
cd /opt/openstack-ansible

```

---

## ✅ Step 4: Bootstrap OpenStack

Run the bootstrap scripts:

```bash
cd /opt/openstack-ansible

./scripts/bootstrap-ansible.sh
./scripts/bootstrap-aio.sh
```
---

> ⚠️ **Note: Locale Encoding Error Fix**

If you encounter the following error during setup:

```
ERROR: Ansible requires the locale encoding to be UTF-8; Detected ISO8859-1.
```

Follow these steps to fix it:

```bash
sudo apt update
sudo apt install locales -y
sudo locale-gen en_US.UTF-8
sudo update-locale LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8
```

Then reboot your system:

```bash
sudo reboot
```

After reboot, verify your locale:

```bash
locale
```

You should see:

```
LANG=en_US.UTF-8
LC_ALL=en_US.UTF-8
```

Now, re-run the script and continue the installation.


---

## ✅ Step 5: Install OpenStack

You can optionally customize the config in `/etc/openstack_deploy`, or continue with the defaults:

```bash
openstack-ansible openstack.osa.setup_hosts
openstack-ansible openstack.osa.setup_infrastructure
openstack-ansible openstack.osa.setup_openstack
```
![Screenshot from 2025-04-16 05-37-08](https://github.com/user-attachments/assets/1654f34c-402d-4abb-8b0a-cc5110bf1b72)


---

## ✅ Post-Installation: Verify and Access

### ✔️ Check LXC containers:

```bash
lxc-ls --fancy
```
![Screenshot from 2025-04-16 05-37-17](https://github.com/user-attachments/assets/ed82ab10-49a6-48b7-a64c-060802104e71)


### ✔️ Get Admin Password:

```bash
cat /etc/openstack_deploy/user_secrets.yml | grep "keystone_auth_admin_password"
```

### ✔️ Access Horizon Dashboard:

Open your browser and go to:

```
http://<your-public-ip>/horizon
```

Login using the admin credentials.

---

## ✅ Manage Virtual Machines

### ✔️ List all VMs:

```bash
virsh list --all
```

You can now create VMs using either the Horizon dashboard or the OpenStack CLI.
![Screenshot from 2025-04-16 05-35-44](https://github.com/user-attachments/assets/b1412b27-402d-4e83-bfc8-2d3bb7d0bd01)
![Screenshot from 2025-04-21 14-22-03](https://github.com/user-attachments/assets/78fb79de-4f3e-447f-849e-c192bbee4631)
![Screenshot from 2025-04-21 09-50-48](https://github.com/user-attachments/assets/234bf390-dabf-4e15-b720-41a4cc196cc7)


---

## 🚀 You're Ready to Use OpenStack!

This setup provides a full OpenStack environment running in LXC containers. Perfect for testing, development, or learning purposes.
