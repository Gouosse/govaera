# 🌍 Govaera

**Govaera** est une plateforme universelle et multidisciplinaire, construite avec une architecture backend (PHP), frontend et base de données (PostgreSQL), orchestrée par **Docker Compose** pour assurer reproductibilité et déploiement simple.  
Au-delà du code, Govaera porte une vision globale : relier **technologie, science, recherche, emploi et économie numérique** dans un seul écosystème.

---

## 🚀 Vision
Govaera n’est pas seulement un projet technique. C’est une idée vivante qui vise à :
- Créer un socle technologique solide et reproductible.
- Offrir un espace scientifique pour partager et collaborer.
- Devenir un hub d’opportunités (emploi, projets, open source).
- Intégrer des solutions de paiement et soutenir l’économie numérique.
- Relier disciplines et cultures dans une plateforme universelle.

---

## ⚙️ Architecture technique
- **Backend (PHP)** : API exposée sur le port `8080`.
- **Frontend** : interface utilisateur exposée sur le port `80`.
- **Base de données (PostgreSQL)** : stockage persistant avec volumes Docker.
- **Docker Compose** : orchestration des services et réseau interne sécurisé (`govaera-net`).
- **Variables sensibles** : externalisées dans un fichier `.env`.

---

## 📂 Structure du dépôt
- `README.md` : présentation et instructions.
- `LICENSE` : licence MIT.
- `docker-compose.yml` : définition des services.
- `.env.example` : modèle de configuration.
- `.gitignore` : exclusion des fichiers sensibles.
- `CONTRIBUTING.md` : guide pour les collaborateurs.
- `.github/workflows/ci.yml` : automatisation CI/CD avec GitHub Actions.

---

## 🔧 Installation et utilisation
1. **Cloner le dépôt** :
   ```bash
   git clone https://github.com/Gouosse/govaera.git
   cd govaerayaml
version: '3.8'

services:
  php:
    build: ./backend/api
    container_name: govaera-php
    depends_on:
      - db
    networks:
      - govaera-net
    ports:
      - "8080:8080"
    environment:
      DB_HOST: db
      DB_USER: ${DB_USER}
      DB_PASSWORD: ${DB_PASSWORD}
      DB_NAME: ${DB_NAME}

  frontend:
    build: ./frontend
    container_name: govaera-frontend
    networks:
      - govaera-net
    ports:
      - "80:80"

  db:
    image: postgres:15
    container_name: govaera-db
    environment:
      POSTGRES_DB: ${DB_NAME}
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - govaera-net

networks:
  govaera-net:

volumes:
  db_data:
