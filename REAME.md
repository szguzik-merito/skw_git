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

### 🔹 Usunięcie lokalnego tagu
```bash
git tag -d v1.0
```

### 🔹 Usunięcie zdalnego tagu
```bash
git push --delete origin v1.0
```

---

## 📌 8. Cofanie zmian
### 🔹 Odwracanie zmian wprowadzonego commita (zachowuje historię)
```bash
git revert HASH
```

### 🔹 Resetowanie repozytorium do wcześniejszego commita (traci historię)
⚠ **Nieodwracalna operacja, która usuwa historię zmian!**
```bash
git reset --hard HASH
```

📌 **Opcje:**
- `--hard` – Resetuje zarówno historię commitów, jak i zmiany w plikach roboczych.

---

## 📌 9. Praca z `stash` (tymczasowe przechowywanie zmian)
### 🔹 Schowanie bieżących, niezacommitowanych zmian:
```bash
git stash
```

### 🔹 Dodanie krótkiego opisu do `stash`:
```bash
git stash push -m "wiadomość"
```

📌 **Opcje:**
- `-m "message"` – Dodaje wiadomość do `stash`.

---

## ✅ Podsumowanie
Powyższe polecenia pozwalają na kompleksowe zarządzanie repozytorium Git, od konfiguracji użytkownika, przez pracę z commitami, gałęziami i zdalnymi repozytoriami, aż po cofanie zmian i operacje na `stash`. 

💡 **Praca z Git jest potężnym narzędziem – pamiętaj, aby regularnie commitować i wypychać zmiany!** 🚀

