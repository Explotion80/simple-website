# Simple Blueprint Website

## Opis projektu
Ten projekt przedstawia **statyczną stronę internetową** stylizowaną na szkic maszyny F1.  
Celem projektu jest nauka i praktyka **DevOps**:

- Tworzenie statycznych stron HTML/CSS
- Konteneryzacja za pomocą Docker
- Automatyzacja CI/CD z GitHub Actions
- Wysyłka obrazów do GitHub Container Registry (GHCR)
- Uruchomienie strony lokalnie lub w środowisku testowym

---

## Kroki tworzenia projektu

### 1️⃣ Tworzenie strony
- Stworzono prosty HTML i CSS:
  - Nagłówek, sekcja główna, animacje SVG
  - Kolorystyka: biel, odcienie niebieskiego i szarości
  - Animacje linii przypominające schemat bolidu F1

---

### 2️⃣ Docker – konteneryzacja
- Utworzono `Dockerfile`:
```
FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
```


GitHub Actions – CI/CD
Workflow .github/workflows/deploy.yml automatyzuje:

Checkout repo
Build obrazu Docker
Logowanie do GHCR
Push obrazu do GHCR
Przykładowa konfiguracja loginu do GHCR:

- name: Log in to GitHub Container Registry
  uses: docker/login-action@v2
  with:
    registry: ghcr.io
    username: ${{ github.actor }}
    password: ${{ secrets.GHCR_PAT }}


Publikacja obrazu:
```
ghcr.io/explotion80/simple-website/simple-website:latest
```
Uruchomienie kontenera z GHCR:
```
docker run -d -p 8080:80 ghcr.io/explotion80/simple-website/simple-website:latest
```


Dobre praktyki DevOps zastosowane w projekcie:

Minimalny, lekki obraz Docker (nginx:alpine)
Automatyzacja workflow z CI/CD
Wersjonowanie obrazów i deployment do GHCR
Oddzielenie frontendu (HTML/CSS) od serwera (Docker + Nginx)
Przygotowanie do rozbudowy: monitoring, testy HTML/CSS, deployment na serwerze lub w chmurze
