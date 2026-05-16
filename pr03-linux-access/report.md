# ПР №3. Управление доступом в Linux

## 1. Создание пользователей

Были созданы пользователи:
- alice
- bob
- carol

Использованные команды:

sudo useradd -m alice
sudo useradd -m bob
sudo useradd -m carol

Для пользователей были установлены пароли:

sudo passwd alice
sudo passwd bob
sudo passwd carol

---

## 2. Создание группы

Была создана группа securegrp:

sudo groupadd securegrp

Пользователи alice и bob были добавлены в группу:

sudo usermod -aG securegrp alice
sudo usermod -aG securegrp bob

Проверка групп:

groups alice
groups bob

---

## 3. Настройка прав доступа

Была создана директория:

sudo mkdir /secure_data

Назначен владелец и группа:

sudo chown alice:securegrp /secure_data

Настроены права доступа:

sudo chmod 770 /secure_data

Проверка:

ls -ld /secure_data

Результат:

| Пользователь | Доступ |
|---|---|
| alice | Полный доступ |
| bob | Доступ разрешён |
| carol | Доступ запрещён |

---

## 4. Настройка ACL

Для пользователя carol были выданы права через ACL:

sudo setfacl -m u:carol:rwx /secure_data

Проверка ACL:

getfacl /secure_data

После настройки ACL пользователь carol получил доступ к директории.

---

## 5. Настройка sudo

Пользователь bob был добавлен в группу sudo:

sudo usermod -aG sudo bob

Проверка:

groups bob

Проверка sudo-доступа:

sudo whoami

Результат:

root

---

## 6. PAM

Модуль pam_unix.so используется для проверки пароля пользователя.

Ключевое слово required означает, что модуль обязательно должен быть успешно выполнен.

Минимальную длину пароля можно настроить через параметр minlen=12 в модуле pam_pwquality.

## 7. Вывод

В ходе выполнения практической работы были изучены:
- создание пользователей и групп;
- управление правами доступа в Linux;
- использование chmod;
- настройка ACL;
- управление sudo-доступом.
