# Конфигурация виртуальной машины devops-vm

## 1. Параметры машины
- ОЗУ: 2048 МБ
- Ядра CPU: 2
- Диск: 25 ГБ, динамически расширяемый
- ОС: Ubuntu Server 24.04 LTS
- Имя ВМ: devops-vm

## 2. Сетевые интерфейсы
- Адаптер 1 (NAT): IP 10.0.2.15, доступ в Интернет.
- Адаптер 2 (Host-only): IP 192.168.56.108, доступ с хостовой машины.

## 3. Правило проброса портов
- Порт хоста: 2222
- Порт гостя: 2222
- Назначение: SSH

## 4. Учётные записи
- student: группы student, sudo. Вход по паролю.
- devops: группы devops, sudo. Вход по ключу `~/.ssh/devops_vm`.

## 5. Служба SSH
- Порт: 2222
- Файл: /etc/ssh/sshd_config.d/99-hardening.conf
- Директивы: PermitRootLogin no, PasswordAuthentication no, PubkeyAuthentication yes, MaxAuthTries 3, AllowUsers devops.

## 6. Правила межсетевого экрана
- Политики по умолчанию: deny incoming, allow outgoing.
- Правила: limit 2222/tcp (SSH), allow 80/tcp (HTTP), allow 443/tcp (HTTPS).
- Логирование: medium.

## 7. Снимки состояния
- 01-clean-install: чистая установка.
- 02-keys-configured: настроены ключи.
- 03-ssh-hardened: усилена защита SSH.