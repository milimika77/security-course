# ПР №4. Аудит событий безопасности Linux

## 1. Установка и запуск auditd

Были установлены пакеты:

sudo apt-get install -y auditd audispd-plugins

Запуск службы:

sudo systemctl enable --now auditd

Проверка статуса:

sudo systemctl status auditd

Результат: служба auditd активна и находится в состоянии active (running).

---

## 2. Анализ журналов systemd-journald

Просмотр последних записей:

journalctl -n 10

Просмотр sudo-событий:

journalctl _COMM=sudo -n 10

Просмотр ошибок:

journalctl -p err -n 10

---

## 3. Настройка auditd

Было добавлено правило аудита:

sudo auditctl -w /srv/project/code -p war -k project_monitor

Проверка правил:

sudo auditctl -l

---

## 4. Анализ событий безопасности

Для генерации события был выполнен тест:

su - bob -c 'echo hacked >> /srv/project/code/test.txt'

Поиск события:

sudo ausearch -k project_monitor -i

### Значение полей ausearch

| Поле | Значение |
|---|---|
| uid | текущий пользователь |
| auid | пользователь, выполнивший вход |
| exe | исполняемый файл |
| comm | выполненная команда |

---

## 5. Анализ логов

Просмотр auth.log:

sudo tail -n 20 /var/log/auth.log

Просмотр неудачных входов:

sudo lastb

Просмотр последних входов:

last -a | head

---

## 6. PAM

Просмотр PAM-конфигурации:

cat /etc/pam.d/login

cat /etc/pam.d/common-password

### Основные параметры

| Параметр | Назначение |
|---|---|
| required | модуль должен выполниться успешно |
| pam_unix.so | проверка локального пароля |
| pam_pwquality.so | политика сложности пароля |

---

## 7. Вывод

В ходе выполнения работы были изучены:
- система auditd;
- журналирование событий Linux;
- анализ логов безопасности;
- PAM-модули аутентификации;
- аудит действий пользователей.
