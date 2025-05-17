# 🚀 Proxmox Ubuntu 24.04 LXC Container Creator
## 🌐 Language / Dil

[🇬🇧 English](#english-version) | [🇹🇷 Türkçe](#türkçe-versiyon)

---

## 📘 English Version

This Ansible playbook automates the creation of multiple Ubuntu 24.04 LXC containers on a Proxmox VE node.

---

## 📋 Requirements

- A running **Proxmox VE** instance with the `ubuntu-24.04-standard` LXC template downloaded.
- **Ansible** installed on the control machine.
- SSH access to the Proxmox host (tested with `root@pam`).
- Python 3.x on the control machine.
- `requests` and `urllib3` Python libraries installed (used by `community.general.proxmox` modules).
- Environment variables for Proxmox credentials and container settings.

---

## 📦 Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/your-username/proxmox-ubuntu-lxc-creator.git
   cd proxmox-ubuntu-lxc-creator
   ```
2. Install required Python dependencies:
    ```bash
    pip install requests urllib3

    ```
3. Install the required Ansible Collections:
    ```bash

    ansible-galaxy collection install community.general
    ```

---
## ⚙️ Configuration

1. Copy the .env.sample file and create your own .env:

    ```bash
    cp .env.sample .env
    ```
2. Edit the .env file with your Proxmox API credentials and desired container password:
    ```bash

    PROXMOX_USER=root@pam
    PROXMOX_PASS=your_password
    PROXMOX_HOST=your_proxmox_ip
    PROXMOX_PORT=8006
    CONTAINER_PASS=your_container_password

    ```
3. Export environment variables before running the playbook:
    ```bash
    export $(grep -v '^#' .env | xargs)
    
    ```
---
## 🖥️ Inventory
Make sure your inventory file (inventory.ini) containers the IP address of your Proxmox node, like tihs;
 ```bash
[proxmox]
your.proxmox.ip ansible_user=root ansible_ssh_pass=your_ssh_password
 ```

## 🚀 Usage
To create containers on Proxmox, simply run:
```bash
ansible-playbook -i inventory.ini create-containers.yml
```
By Default, the playbook creates 5 Ubuntu 24.04 containers in a loop. You can customize the loop or container parameters in the `create-containers.yml`

---

## 📁 Project Structure
```bash
proxmox-ubuntu-lxc-creator/
├── .env.sample           # Sample environment variables file
├── inventory.ini         # Ansible inventory file
├── playbook.yml          # Main Ansible playbook
├── README.md             # Project documentation


```

## 🛡️ Notes
- This playbook assumes Proxmox's `ubuntu-24.04-standard_*.tar.zst` template is downloaded and available in local:vztmpl/.
- The `.env` file must be exported before running the playbook, otherwise it won’t authenticate correctly.
- Passwords and secrets should never be committed to version control — always use `.env.`

---

## 🤝 Contributing
Feel free to fork this repo, make changes, and open a pull request!

---

## 📗 Türkçe versiyon

# 🚀 Proxmox Ubuntu 24.04 LXC Container Oluşturucu
Bu Ansible playbook'u, bir Proxmox VE node üzerinde birden fazla Ubuntu 24.04 LXC container oluşturma işlemini otomatikleştirir.

---

## 📋 Gereksinimler

- İndirilmiş `ubuntu-24.04-standard` LXC template'ine sahip, çalışan bir **Proxmox VE** instance'ı.
- Kontrol makinesinde kurulu **Ansible**.
- Proxmox host'una SSH erişimi ( `root@pam` ile test edilmiştir).
- Kontrol makinesinde Python 3.x.
- `requests` ve `urllib3` Python kütüphanelerinin kurulu olması (`community.general.proxmox` modülleri tarafından kullanılır).
- Proxmox kimlik bilgileri ve container ayarları için ortam değişkenleri (Environment variables).

---

## 📦 Kurulum

1.  Bu repoyu klonlayın:
    ```bash
    git clone [https://github.com/your-username/proxmox-ubuntu-lxc-creator.git](https://github.com/your-username/proxmox-ubuntu-lxc-creator.git)
    cd proxmox-ubuntu-lxc-creator
    ```
2.  Gerekli Python bağımlılıklarını kurun:
    ```bash
    pip install requests urllib3
    ```
3.  Gerekli Ansible Collections'ı kurun:
    ```bash
    ansible-galaxy collection install community.general
    ```

---

## ⚙️ Yapılandırma

1.  `.env.sample` dosyasını kopyalayarak kendi `.env` dosyanızı oluşturun:

    ```bash
    cp .env.sample .env
    ```
2.  `.env` dosyasını Proxmox API kimlik bilgileriniz ve istediğiniz container parolası ile düzenleyin:
    ```bash
    PROXMOX_USER=root@pam
    PROXMOX_PASS=sizin_parolaniz
    PROXMOX_HOST=sizin_proxmox_ipniz
    PROXMOX_PORT=8006
    CONTAINER_PASS=sizin_container_parolaniz
    ```
3.  Playbook'u çalıştırmadan önce ortam değişkenlerini export edin:

    ```bash
    export $(grep -v '^#' .env | xargs)

    ```

---

## 🖥️ Envanter (Inventory)
Envanter dosyanızın (`inventory.ini`) Proxmox node'unuzun IP adresini aşağıdaki gibi içerdiğinden emin olun;
 ```bash
[proxmox]
sizin.proxmox.ipniz ansible_user=root ansible_ssh_pass=sizin_ssh_parolaniz

```

## 🚀 Kullanım
Proxmox üzerinde container'ları oluşturmak için sadece şu komutu kullanın:
```bash

ansible-playbook -i inventory.ini create-containers.yml

```
Varsayılan olarak, playbook bir döngü/loop içinde 5 adet Ubuntu 24.04 container oluşturur. Döngüyü veya container parametrelerini create-containers.yml dosyasında özelleştirebilirsiniz.

## 📁 Proje Dizini
```bash
proxmox-ubuntu-lxc-creator/
├── .env.sample          # Örnek ortam değişkenleri dosyası
├── inventory.ini        # Ansible envanter dosyası
├── create-containers.yml # Ana Ansible playbook'u
├── README.md            # Proje dokümantasyonu
```
---
## 🛡️ Notlar
- Bu playbook, Proxmox'un `ubuntu-24.04-standard_*.tar.zst` template'inin indirilmiş ve `local:vztmpl/` dizininde mevcut olduğunu varsayar.
- Playbook'u çalıştırmadan önce `.env` dosyasının export edilmesi gerekir, aksi takdirde kimlik doğrulama doğru şekilde yapılamaz.
- Parolalar ve gizli bilgiler asla sürüm kontrolüne (version control) commit edilmemelidir, her zaman `.env` kullanın.
---

## 🤝 Katkıda Bulunma
Bu repoyu dilediğiniz gibi forklayabilir özelleştirebilirsiniz ❤️s



