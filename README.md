# Cloud-Init-VM-Proxmox
Установка Ubuntu Cloud-Init VM в Proxmox
🧩 Что мы получим в итоге

-Ubuntu Server (cloud image)

-Без ISO-установки

-Автонастройка через Cloud-Init

-Доступ по SSH

-Шаблон (Template) для клонов / Terraform
Требования

-Proxmox установлен

-Доступ в Web UI и Shell

-VM ID (пример: 103)

-Storage:

-local (directory)

-local-lvm (LVM)
2️⃣ Скачиваем Ubuntu Cloud Image (ПРАВИЛЬНО)
🔹 Открываем Shell Proxmox
🔹 Скачиваем образ
```bash
cd /var/lib/vz
mkdir -p template/qemu
cd template/qemu

wget https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img
```
3️⃣ Создаём пустую ВМ (БЕЗ ДИСКОВ)
В Web UI → Create VM
1. General
```bash
VM ID: 103

Name: ubuntu-cloud
```
2. OS
```bash
Do not use any media ❗
```
3. System

```bash
Machine: q35

BIOS: OVMF (UEFI)

Add EFI Disk: ✅
```
4. Disks
```bash
4️⃣ Disks

Device: VirtIO Block

Storage: любой

Disk size: 10–20 GB
```
5. CPU
```bash
Cores: 2
```
6. Memory
```bash
RAM: 4096 MB
```
7. Network
```
Model: VirtIO

Bridge: vmbr0
```
8. Confirm
```bash
✔ Finish
```
4️⃣ Импортируем Cloud Image в ВМ
```ash
qm importdisk 103 /var/lib/vz/template/qemu/jammy-server-cloudimg-amd64.img local-lvm
```

5️⃣ Подключаем диск как ОС
```bash
qm set 103 --scsi0 local-lvm:vm-103-disk-0
(если имя другое — смотри qm config 103)
```

6️⃣ Удаляем лишний диск (если есть)
```bash
qm set 103 --delete virtio0
```
7️⃣ Добавляем Cloud-Init диск
```bash
qm set 103 --ide2 local-lvm:cloudinit
```
8️⃣ Boot Order
```bash
qm set 103 --boot "order=scsi0;ide2;net0"
```
9️⃣ Настройка Cloud-Init (GUI)

VM → Cloud-Init

Заполни:

-User: ubuntu

-Password: ❌ (лучше без)

-SSH public key: ✅

-IP Config: DHCP

-👉 Regenerate Image
🔟 Запуск ВМ
```bash
qm start 103
```
1️⃣1️⃣ (РЕКОМЕНДУЕТСЯ) QEMU Guest Agent
```bash
sudo apt update
sudo apt install qemu-guest-agent -y
sudo systemctl enable --now qemu-guest-agent
```
В Proxmox:
```bash
VM → Options → QEMU Guest Agent → Enabled
```
