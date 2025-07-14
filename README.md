# Backend Flask – Exam OCR Agent

Ten projekt przyjmuje zdjęcie dokumentu, wykonuje OCR w Google Cloud Vision,
zapisuje wyniki do Excela i wysyła e‑mail z załącznikiem Excel.

## Szybki start lokalnie

1. Zainstaluj zależności  
   ```bash
   pip install -r requirements.txt
   ```
2. Ustaw zmienne środowiskowe (lub stwórz plik .env):
   * `GOOGLE_APPLICATION_CREDENTIALS=google_credentials.json`
   * `GMAIL_USER=pablo.al3435@gmail.com`
   * `GMAIL_PASS=<Twoje 16‑znakowe hasło aplikacji>`
3. Uruchom serwer
   ```bash
   python app.py
   ```
4. Wyślij POST `multipart/form-data`:
   * pole `file` – obraz,
   * opcjonalnie `to` – adres odbiorcy.

## Deploy na Render.com (Free)

1. **Przygotuj repozytorium GitHub:**
    * Umieść pliki tego projektu.
    * Dodaj `google_credentials.json` do repozytorium **(lub lepiej do sekcji Secrets w Render).**

2. **Utwórz Web Service:**
    * Type: `Web Service`
    * Runtime: `Python`
    * Build Command: `pip install -r requirements.txt`
    * Start Command: `gunicorn app:app`
    * Branch: `main`

3. **Environment vars (Render → Environment):**
    | Key                           | Value                               |
    | ----------------------------- | ----------------------------------- |
    | `GMAIL_USER`                 | `pablo.al3435@gmail.com`            |
    | `GMAIL_PASS`                 | `<16‑znakowe hasło aplikacji>`      |
    | `GOOGLE_APPLICATION_CREDENTIALS` | `google_credentials.json`        |

    > Jeśli umieścisz plik JSON w repozytorium, Render znajdzie go w ścieżce roboczej.

4. **Deploy** – Render po zbudowaniu poda publiczny URL, np.  
   `https://exam-ocr-agent.onrender.com`

5. **Test** – wyślij zapytanie:
   ```bash
   curl -X POST -F "file=@test.jpg" -F "to=docelowy@example.com"        https://exam-ocr-agent.onrender.com/upload
   ```

## Struktura

```
backend-flask/
├── app.py
├── requirements.txt
└── README.md
```

***Good luck & happy coding!***