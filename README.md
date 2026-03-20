# govaera
Projet GOVAERA- backend et frontend avec Docker

yaml
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
      DB_HOST=db
      DB_USER=govaera_user
      DB_PASSWORD=MotDePasseFort123!
      DB_NAME=govaera

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
      POSTGRES_DB: govaera
      POSTGRES_USER: govaera_user
      POSTGRES_PASSWORD: MotDePasseFort123!
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - govaera-net

networks:
  govaera-net:

volumes:
  db_data:
bash
git clone https://github.com/<ton-username>/<nom-du-repo>.git
cd <nom-du-repo>

bash
git add README.md
git commit -m "Mise à jour README.md - ajout science et vision globale"
git push origin main


