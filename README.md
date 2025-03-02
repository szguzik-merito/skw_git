# 🛠️ KONFIGURACJA UŻYTKOWNIKA GITA

## 📌 1. Ustawianie nazwy użytkownika oraz adresu e-mail

Przed rozpoczęciem pracy z Git warto skonfigurować dane użytkownika:

```bash
git config --global user.name "Jan Kowalski"
git config --global user.email "youremail@domain.com"
```

---

## 📌 2. Inicjalizacja repozytorium

Aby utworzyć nowe repozytorium Git w bieżącym katalogu:

```bash
git init
```

---

## 📌 3. Dodawanie i zatwierdzanie zmian

### 🔹 Dodanie zmian do indeksu (staging area)

Dodanie **wszystkich** nowych, zmienionych i usuniętych plików w bieżącym katalogu:

```bash
git add .
```

Dodanie **wszystkich** plików w całym repozytorium (równoważne `git add .`):

```bash
git add -A
```

### 🔹 Zatwierdzanie zmian

Tworzenie commita z wiadomością (możesz zmienić `"first commit"` na własną treść):

```bash
git commit -m "first commit"
```

📌 **Opcje:**

- `-m "message"` – Dodaje wiadomość do commita.

---

## 📌 4. Praca z gałęziami

### 🔹 Zmiana nazwy bieżącej gałęzi na `main`

```bash
git branch -M main
```

📌 **Opcje:**

- `-M` – Nadpisuje istniejącą gałąź o podanej nazwie.

### 🔹 Tworzenie nowej gałęzi `develop`

```bash
git branch develop
```

### 🔹 Przełączanie się na inną gałąź

```bash
git checkout develop
```

📌 **Opcje:**

- `checkout` – Pozwala przełączać się pomiędzy istniejącymi gałęziami.

### 🔹 Scalanie zmian z `develop` do `main`

```bash
git merge develop
```

---

## 📌 5. Praca ze zdalnym repozytorium

### 🔹 Dodanie zdalnego repozytorium o nazwie `origin`

Pamiętaj, aby podmienić `URL` na adres swojego repozytorium:

```bash
git remote add origin http://github.com/szguzik/empty-project.git
```

Repozytorium może mieć więcej niż jeden adres, dlatego możesz dodać kolejne:

```bash
git remote add origin2 http://github.com/szguzik/empty-project-2.git
```

Jeśli używasz SSH:

```bash
git remote add origin git@github.com:szguzik-wsb/test-repo.git
```

### 🔹 Sprawdzenie listy zdalnych repozytoriów

```bash
git remote -v
```

### 🔹 Pobieranie zmian z zdalnego repozytorium

```bash
git fetch origin
```

### 🔹 Pobranie i scalanie zmian

```bash
git pull origin main
```

### 🔹 Zmiana adresu zdalnego repozytorium

```bash
git remote set-url origin git@github.com:szguzik-wsb/test-repo.git
```

---

## 📌 6. Wypychanie zmian na zdalne repozytorium

```bash
git push origin main
```

---

## 📌 7. Praca z tagami

### 🔹 Tworzenie nowego tagu

```bash
git tag -a v1.0 -m "Wersja 1.0"
```

📌 **Opcje:**

- `-a` – Tworzy tag z adnotacją.
- `-m "message"` – Dodaje wiadomość do tagu.

### 🔹 Wypchnięcie tagu do zdalnego repozytorium

```bash
git push origin v1.0
```

### 🔹 Lista tagów w repozytorium

```bash
git tag
```

### 🔹 Przełączanie się na tag

```bash
git checkout v1.0
```

### 🔹 Tworzenie nowej gałęzi na podstawie tagu

```bash
git checkout -b new-branch v1.0
```

### 🔹 Usunięcie lokalnego tagu

```bash
git tag -d v1.0
```

### 🔹 Usunięcie zdalnego tagu

```bash
git push --delete origin v1.0
```

---

## 📌 8. Praca z kluczami SSH

### 🔹 Generowanie wielu kluczy SSH

Jeśli używasz różnych kont GitHub/GitLab, możesz utworzyć osobne klucze SSH dla każdego konta.
Dla konta **personalnego**:

```bash
ssh-keygen -t rsa -b 4096 -C "personal@example.com" -f ~/.ssh/id_rsa_personal
```

Dla konta **służbowego**:

```bash
ssh-keygen -t rsa -b 4096 -C "work@example.com" -f ~/.ssh/id_rsa_work
```

📌 **Opcje:**
- `-t rsa` – Określa typ klucza (RSA).
- `-b 4096` – Ustawia długość klucza na 4096 bitów.
- `-C "email"` – Dodaje komentarz (zazwyczaj adres e-mail).
- `-f ~/.ssh/id_rsa_nazwa` – Określa nazwę i ścieżkę pliku klucza.

Po wygenerowaniu kluczy dodaj ich zawartość (`id_rsa_personal.pub` i `id_rsa_work.pub`) do odpowiednich kont na GitHub/GitLab.

### 🔹 Konfiguracja pliku SSH `config`

Aby Git mógł używać odpowiednich kluczy, skonfiguruj plik `~/.ssh/config`:

```plaintext
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_personal

Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_work
```

📌 **Opis konfiguracji:**
- `Host github-personal` – Alias dla konta personalnego.
- `HostName github.com` – Serwer, do którego łączysz się przez SSH.
- `User git` – Użytkownik GitHub/GitLab przy połączeniu przez SSH.
- `IdentityFile ~/.ssh/id_rsa_personal` – Ścieżka do klucza prywatnego.

### 🔹 Użycie wielu kluczy SSH

Po skonfigurowaniu `~/.ssh/config` możesz używać odpowiedniego klucza dla konkretnego repozytorium:

Dla konta personalnego:

```bash
git clone git@github-personal:username/repo.git
```

Dla konta służbowego:

```bash
git clone git@github-work:company/repo.git
```

📌 **Sprawdzenie aktywnego klucza:**
Jeśli chcesz sprawdzić, który klucz SSH jest używany do połączenia:

```bash
ssh -T git@github.com
```

To pozwala na łatwe przełączanie się między różnymi kluczami SSH w zależności od repozytorium.

---

## ✅ Podsumowanie

Powyższe polecenia pozwalają na kompleksowe zarządzanie repozytorium Git, od konfiguracji użytkownika, przez pracę z commitami, gałęziami i zdalnymi repozytoriami, aż po cofanie zmian i operacje na `stash`.

💡 **Praca z Git jest potężnym narzędziem – pamiętaj, aby regularnie commitować i wypychać zmiany!** 🚀

