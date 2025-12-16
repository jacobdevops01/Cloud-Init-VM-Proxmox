📘 Документация: Cloud-Init в Proxmox из видео (пошагово)
🧠 Что будет в итоге

✔️ Готовый Cloud-Init шаблон VM
✔️ Автоматическая настройка пользователей и сети
✔️ Быстрое клонирование ВСЕХ ВМ с разными параметрами

📦 1. Подготовка
📥 Скачиваем Ubuntu Cloud-image

Можно через браузер или через Proxmox Shell:
```bash
wget https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img
```
Это готовый образ с поддержкой Cloud-Init.
🛠 2. Создание VM-заходки под шаблон

В интерфейсе Proxmox Create VM:

📌 Basic settings:
<img width="715" height="539" alt="1" src="https://github.com/user-attachments/assets/a677b250-ee50-4c09-a9f5-94f2388d2ea7" />
<img width="715" height="533" alt="{574A9B68-CF0C-44EC-9F47-827CB0F8D0B6}" src="https://github.com/user-attachments/assets/c5c7a2d6-31d7-4fae-b8c2-458754a7a25f" />
<img width="714" height="533" alt="2" src="https://github.com/user-attachments/assets/eaaa71cb-312e-4606-ab56-43c0b1e55236" />
<img width="620" height="462" alt="4" src="https://github.com/user-attachments/assets/30686c6c-b46b-4368-85d1-13e2b0198cf7" />
<img width="622" height="459" alt="5" src="https://github.com/user-attachments/assets/40cf105c-04ed-4d68-9967-696847b4e8d3" />
<img width="622" height="464" alt="6" src="https://github.com/user-attachments/assets/f4dbf619-1261-4436-8059-9e907261f72b" />
<img width="722" height="539" alt="{C3EE4AEB-6DC4-4AF5-8315-38A7758D3D30}" src="https://github.com/user-attachments/assets/5a9be131-8f9f-40d1-a406-0fcf86fa3201" />
<img width="711" height="523" alt="{E3AD41BE-96A1-48F4-9F3B-454749F707B6}" src="https://github.com/user-attachments/assets/0bae7fee-a42a-418e-88bd-1671391a8220" />
<img width="622" height="462" alt="7" src="https://github.com/user-attachments/assets/f53c2d63-7ff6-4bf4-9bb0-a0e87e5bf44c" />
☁ 3. Импорт cloud-image в VM

После создания VM:

Через CLI:
```bash
qm importdisk 999 jammy-server-cloudimg-amd64.img local-lvm
```
Это добавляет образ в local-lvm.

📀 4. Настройка VM disks

Подключаем импортированный диск как основной:
```bash
qm set 999 --scsihw virtio-scsi-pci \
           --scsi0 local-lvm:vm-999-disk-0
```
Добавляем диск Cloud-Init:
```bash
qm set 999 --ide2 local-lvm:cloudinit
```
И настраиваем порядок загрузки:
```bash
qm set 9000 --boot c --bootdisk scsi0
```
Добавляем консоль:
```bash
qm set 9000 --serial0 socket --vga serial0
```
Это чтобы было удобно смотреть вывод.

СРАЗУ увеличиваем диск до 20 GB
```bash
qm resize 999 scsi0 20G
```
