# eks-deploy.yml
Deploy para new services
name: Taggify EKS Deploy

on:
  workflow_dispatch:
  push:
    branches:
      - main
      - qa

permissions:
  id-token: write
  contents: write

jobs:
  staging:
    name: Deploy STAGING Environment
    if: ${{ github.ref == 'refs/heads/qa' }}
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set Up Kafka
        run: |
          echo "Setting up Kafka brokers and queues..."
          # Aquí se configurará Kafka con las colas necesarias según el diagrama.

      - name: Deploy PostgreSQL
        run: |
          echo "Deploying PostgreSQL database..."
          # Script para iniciar la base de datos y migraciones necesarias.

      - name: Deploy Clickhouse
        run: |
          echo "Deploying Clickhouse for analytics..."
          # Script para iniciar la base de datos Clickhouse.

      - name: Deploy Microservices
        run: |
          echo "Building and deploying microservices (Screen Collector, DSP API, etc.)..."
          # Comandos para construir y desplegar SCREEN-COLLECTOR y DSP-SCREEN-API.

      - name: Deploy Geo-Resolver
        run: |
          echo "Deploying Geo-Resolver service..."
          # Comandos para implementar el servicio de resolución geográfica.

      - name: Integrate with Google Geo Services
        run: |
          echo "Integrating with Google Geo Services and OpenStreetMap..."
          # Configuración para integrarse con APIs externas.

  production:
    name: Deploy PRODUCTION Environment
    if: ${{ github.ref == 'refs/heads/main' }}
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set Up Kafka
        run: |
          echo "Setting up Kafka brokers and queues for production..."
          # Configuración de Kafka para producción.

      - name: Deploy PostgreSQL
        run: |
          echo "Deploying PostgreSQL database for production..."
          # Scripts de migración y configuración.

      - name: Deploy Clickhouse
        run: |
          echo "Deploying Clickhouse for production analytics..."
          # Configuración de Clickhouse.

      - name: Deploy Microservices
        run: |
          echo "Building and deploying production microservices..."
          # Comandos para desplegar SCREEN-COLLECTOR y DSP-SCREEN-API.

      - name: Deploy Geo-Resolver
        run: |
          echo "Deploying Geo-Resolver service for production..."
          # Despliegue del Geo-Resolver.

      - name: Integrate with Google Geo Services
        run: |
          echo "Integrating with Google Geo Services and OpenStreetMap for production..."
          # Configuración para producción de APIs externas.
