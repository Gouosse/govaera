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
