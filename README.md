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
<img width="717" height="533" alt="3" src="https://github.com/user-attachments/assets/0516cb37-1841-4ae9-9bca-24e0673d9fab" />
<img width="620" height="462" alt="4" src="https://github.com/user-attachments/assets/30686c6c-b46b-4368-85d1-13e2b0198cf7" />
<img width="622" height="459" alt="5" src="https://github.com/user-attachments/assets/40cf105c-04ed-4d68-9967-696847b4e8d3" />
<img width="622" height="464" alt="6" src="https://github.com/user-attachments/assets/f4dbf619-1261-4436-8059-9e907261f72b" />
<img width="622" height="462" alt="7" src="https://github.com/user-attachments/assets/f53c2d63-7ff6-4bf4-9bb0-a0e87e5bf44c" />

