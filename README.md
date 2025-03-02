# Podręcznik Git

Kompleksowy przewodnik po najważniejszych poleceniach Git – od konfiguracji użytkownika, poprzez inicjalizację repozytorium, pracę z gałęziami, zdalnymi repozytoriami, tagami, aż po zaawansowane zagadnienia, takie jak rebase, submoduły czy bisect.  

## Spis treści

1. Konfiguracja użytkownika  
2. Inicjalizacja repozytorium  
3. Dodawanie i zatwierdzanie zmian  
4. Praca z gałęziami (Branching)  
5. Zdalne repozytoria (Remote)  
6. Wypychanie zmian (Push)  
7. Praca z tagami (Tagging)  
8. Praca z kluczami SSH  
9. Wyświetlanie historii zmian (Log)  
10. Wycofywanie zmian (Reset, Revert)  
11. Praca ze Schowkiem zmian (Stash)  
12. Praca z submodułami (Submodules)  
13. Git Rebase – modyfikowanie historii commitów  
14. Git Bisect – znajdowanie błędów  
15. Git Aliasy  
16. Dodatkowe wskazówki  
17. Podsumowanie  

---

## 1. Konfiguracja użytkownika

Przed rozpoczęciem pracy z Git należy ustawić nazwę użytkownika oraz adres e-mail, które będą widoczne w historii commitów.

    git config --global user.name "Jan Kowalski"
    git config --global user.email "youremail@domain.com"

**Parametry:**  
- `--global` – Ustawia konfigurację dla całego systemu (wszystkich repozytoriów) użytkownika.

---

## 2. Inicjalizacja repozytorium

Aby utworzyć **nowe repozytorium** Git w bieżącym katalogu, użyj polecenia:

    git init

Po wykonaniu tego polecenia w katalogu pojawi się ukryty folder `.git/`, który przechowuje całą historię zmian.

---

## 3. Dodawanie i zatwierdzanie zmian

### 3.1 Dodawanie zmian do indeksu (staging area)

- Dodanie **wszystkich** nowych, zmienionych i usuniętych plików z bieżącego katalogu:

      git add .

- Dodanie **wszystkich** zmian w całym repozytorium (równoważne powyższemu poleceniu):

      git add -A

### 3.2 Zatwierdzanie zmian (commit)

- Utworzenie commita z wiadomością:

      git commit -m "first commit"

**Parametry:**  
- `-m "message"` – Dodaje wiadomość (opis) do commita.

---

## 4. Praca z gałęziami (Branching)

### 4.1 Zmiana nazwy bieżącej gałęzi na `main`

    git branch -M main

**Parametry:**  
- `-M` – Nadpisuje istniejącą gałąź (jeśli już istnieje o tej nazwie).

### 4.2 Tworzenie nowej gałęzi `develop`

    git branch develop

*(Polecenie tworzy gałąź, ale nie przełącza na nią.)*

### 4.3 Przełączanie się na inną gałąź

    git checkout develop

**Parametry:**  
- `checkout` – Pozwala przełączać się pomiędzy istniejącymi gałęziami oraz przywracać pliki do stanu z wybranego commita.

### 4.4 Scalanie zmian z `develop` do `main`

    git merge develop

---

## 5. Zdalne repozytoria (Remote)

### 5.1 Dodanie zdalnego repozytorium

Najczęściej używaną nazwą dla repozytorium zdalnego jest `origin`.  
Pamiętaj, aby podmienić `URL` na adres swojego repozytorium:

    git remote add origin http://github.com/szguzik/empty-project.git

Możesz dodać kolejne repozytoria, nadając im inne nazwy (np. `origin2`):

    git remote add origin2 http://github.com/szguzik/empty-project-2.git

Jeśli używasz SSH:

    git remote add origin git@github.com:szguzik-wsb/test-repo.git

### 5.2 Sprawdzenie listy zdalnych repozytoriów

    git remote -v

### 5.3 Pobieranie zmian z zdalnego repozytorium

    git fetch origin

### 5.4 Pobranie i scalanie zmian

    git pull origin main

### 5.5 Zmiana adresu zdalnego repozytorium

    git remote set-url origin git@github.com:szguzik-wsb/test-repo.git

---

## 6. Wypychanie zmian (Push)

Aby przesłać (wypchnąć) zmiany z lokalnego repozytorium na zdalne:

    git push origin main

---

## 7. Praca z tagami (Tagging)

### 7.1 Tworzenie nowego tagu

    git tag -a v1.0 -m "Wersja 1.0"

**Parametry:**  
- `-a` – Tworzy tag z adnotacją.  
- `-m "message"` – Dodaje wiadomość do tagu.

### 7.2 Wypchnięcie tagu do zdalnego repozytorium

    git push origin v1.0

### 7.3 Lista tagów w repozytorium

    git tag

### 7.4 Przełączanie się na tag

    git checkout v1.0

### 7.5 Tworzenie nowej gałęzi na podstawie tagu

    git checkout -b new-branch v1.0

### 7.6 Usunięcie lokalnego tagu

    git tag -d v1.0

### 7.7 Usunięcie zdalnego tagu

    git push --delete origin v1.0

---

## 8. Praca z kluczami SSH

### 8.1 Generowanie wielu kluczy SSH

Jeśli używasz różnych kont (np. GitHub/GitLab), możesz utworzyć osobne klucze SSH dla każdego konta.

**Dla konta personalnego:**

    ssh-keygen -t rsa -b 4096 -C "personal@example.com" -f ~/.ssh/id_rsa_personal

**Dla konta służbowego:**

    ssh-keygen -t rsa -b 4096 -C "work@example.com" -f ~/.ssh/id_rsa_work

**Parametry:**  
- `-t rsa` – Typ klucza (RSA).  
- `-b 4096` – Długość klucza (4096 bitów).  
- `-C "email"` – Komentarz (zazwyczaj adres e-mail).  
- `-f ~/.ssh/id_rsa_nazwa` – Ścieżka i nazwa pliku klucza prywatnego.

### 8.2 Konfiguracja pliku `~/.ssh/config`

Aby Git mógł używać odpowiednich kluczy, skonfiguruj plik `~/.ssh/config`:

    Host github-personal
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_personal

    Host github-work
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_work

### 8.3 Użycie wielu kluczy SSH

Po poprawnej konfiguracji możesz klonować i pracować z repozytoriami, używając aliasów:

    git clone git@github-personal:username/repo.git
    git clone git@github-work:company/repo.git

### 8.4 Sprawdzenie aktywnego klucza

    ssh -T git@github.com

---

## 9. Wyświetlanie historii zmian (Log)

### 9.1 Podstawowe polecenia

- Pełna historia commitów:

      git log

- Skrócona historia (jedna linia na commit):

      git log --oneline

- Historia commitów z informacją o zmienionych plikach:

      git log --stat

- Historia commitów dla konkretnego pliku:

      git log -- filename.txt

**Przydatne opcje:**  
- `--oneline` – Wyświetla każdy commit w jednej linii.  
- `--stat` – Wyświetla statystyki zmienionych plików.

---

## 10. Wycofywanie zmian (Reset, Revert)

### 10.1 Usunięcie zmian przed dodaniem do indeksu (staging area)

- Cofnięcie zmian w pojedynczym pliku:

      git checkout -- filename.txt

- Cofnięcie wszystkich niezatwierdzonych zmian:

      git checkout -- .

### 10.2 Usunięcie zmian z indeksu, ale przed commitowaniem

- Wycofanie konkretnych plików z indeksu:

      git reset HEAD filename.txt

- Wycofanie wszystkich plików z indeksu:

      git reset HEAD

### 10.3 Cofnięcie ostatniego commita (lokalnie)

Jeśli commit został już utworzony, ale **nie** został wypchnięty do zdalnego repozytorium:

      git reset --soft HEAD~1

*(Cofnięcie o jeden commit, ale zachowanie zmian w plikach.)*

### 10.4 Gdy commit został już wypchnięty

Jeśli commit został wysłany na zdalne repozytorium, a chcesz go usunąć:

      git reset --hard HEAD~1

*(Trwale usuwa commit i zmiany. Uważaj przy współdzielonym repozytorium.)*

### 10.5 `git revert` – metoda bezpieczna

Zamiast usuwać commit z historii, można stworzyć nowy commit odwracający zmiany:

      git revert HASH

**Przykład:**

      git revert 09gdf09gdf7gd90g7d09fg

*(Tworzy nowy commit, który odwraca zmiany wprowadzone przez wskazany commit.)*

Cofanie **kilku** commitów jednocześnie:

      git revert OLDEST_HASH^..NEWEST_HASH

---

## 11. Praca ze Schowkiem zmian (Stash)

Jeśli masz rozpoczęte, niezacommitowane prace i chcesz je chwilowo odłożyć:

    git stash

### 11.1 Podstawowe polecenia stash

- Wyświetlenie listy zapisanych schowków:

      git stash list

- Przywrócenie zmian z ostatniego schowka:

      git stash apply

- Przywrócenie zmian z konkretnego schowka:

      git stash apply stash@{n}

- Wyciągnięcie zmian i usunięcie schowka:

      git stash pop stash@{n}

- Usunięcie konkretnego schowka bez przywracania zmian:

      git stash drop stash@{n}

- Wyczyścenie całej listy schowków:

      git stash clear

- Dodanie opisu do schowka:

      git stash push -m "opis zmian"

---

## 12. Praca z submodułami (Submodules)

Jeśli w repozytorium przechowujesz inne repozytorium (np. jako zależność), możesz je dodać jako submoduł.

### 12.1 Dodanie submodułu

    git submodule add https://github.com/example/repo.git submodules/repo

### 12.2 Pobranie submodułów

    git submodule update --init --recursive

### 12.3 Aktualizacja submodułów

    git submodule update --remote

---

## 13. Git Rebase – modyfikowanie historii commitów

`rebase` pozwala na zmianę (przepisanie) historii commitów, np. scalenie kilku commitów w jeden.

### 13.1 Tryb interaktywny

    git rebase -i HEAD~3

- `-i` (interactive) – Umożliwia edycję historii commitów.  
- `HEAD~3` – Dotyczy ostatnich 3 commitów.

### 13.2 Po wystąpieniu konfliktów

Jeśli w trakcie rebase pojawią się konflikty, rozwiąż je i kontynuuj:

    git rebase --continue

### 13.3 Anulowanie rebase

    git rebase --abort

---

## 14. Git Bisect – znajdowanie błędów

Pozwala namierzyć commit, w którym pojawił się błąd, stosując podejście binarne.

### 14.1 Rozpoczęcie bisect

    git bisect start
    git bisect bad HEAD
    git bisect good COMMIT_ID

*(Git będzie przeskakiwał między commitami, aby zlokalizować ten wadliwy.)*

### 14.2 Zakończenie bisect

    git bisect reset

---

## 15. Git Aliasy

Jeśli często używasz tych samych poleceń, możesz je skrócić za pomocą aliasów.

### 15.1 Definiowanie aliasów

    git config --global alias.lg "log --oneline --graph --decorate --all"
    git config --global alias.co "checkout"
    git config --global alias.cm "commit -m"
    git config --global alias.st "status"

### 15.2 Użycie aliasów

    git lg
    git co develop
    git cm "Aktualizacja"
    git st

---

## 16. Dodatkowe wskazówki

### 16.1 Plik `.gitignore`
Aby wykluczyć określone pliki lub katalogi z repozytorium (np. pliki tymczasowe, kompilacje, prywatne klucze), dodaj je do pliku `.gitignore`.

Przykładowa zawartość `.gitignore`:

    # Pliki tymczasowe
    *.log
    *.tmp
    
    # Kompilacje
    dist/
    build/

### 16.2 Git Hooks
W katalogu `.git/hooks/` znajdują się skrypty, które uruchamiają się na określone zdarzenia (np. przed commitowaniem – `pre-commit`, po wypchnięciu – `post-push`, itd.). Mogą służyć do automatycznego formatowania kodu, testów lub walidacji.

### 16.3 Analiza zmian w plikach
- `git diff` – Wyświetla różnice między commitami, gałęziami lub stanem roboczym.  
- `git blame` – Pokazuje, kto i kiedy wprowadził zmiany w każdej linii (przydatne w zespole).

---

## 17. Podsumowanie

Powyższy przewodnik zawiera najważniejsze polecenia Git, wzbogacone o informacje dotyczące parametrów i przykłady użycia. W codziennej pracy pamiętaj o:

- **Częstych commitach** – zatwierdzaj zmiany w małych porcjach.
- **Pracy na gałęziach** – rozwijaj nowe funkcje lub poprawiaj błędy na osobnych gałęziach, a następnie scalaj je do `main`.
- **Bezpiecznym wycofywaniu zmian** – korzystaj z `git revert` (zamiast `git reset --hard`) w przypadku współdzielonych repozytoriów.
- **Regularnej synchronizacji** (`git pull` / `git push`).

Dzięki Git możesz zawsze cofnąć lub przerobić historię (w zależności od sytuacji), więc nie bój się eksperymentować – najlepiej na testowym repozytorium. Powodzenia w pracy z Git!
