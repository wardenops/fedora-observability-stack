# 🚀 Fedora Observability Stack (LGP-C Stack)

Este repositorio contiene la configuración necesaria para desplegar un ecosistema completo de Observabilidad y Seguridad de Red en una workstation Fedora. El proyecto nace de la necesidad de identificar dispositivos en la red local (IoT, wearables, móviles) y monitorizar el rendimiento del sistema mediante contenedores.

```
fedora-observability-stack/
├── config/
│   ├── prometheus.yml
│   └── promtail-config.yml
├── scripts/
│   ├── setup.sh        # Instala dependencias (si faltan) y levanta el stack
│   └── cleanup.sh      # Borra contenedores, volúmenes y archivos temporales
├── docker-compose.yml
├── .gitignore
└── README.md
```

## 🛠️ El Stack Tecnológico

He diseñado este entorno utilizando el modelo LGP-C (Loki, Grafana, Prometheus + Containers) orquestado con docker-compose:

- **Grafana**: Visualización centralizada de métricas y eventos.

- **Prometheus**: Base de datos de series temporales para métricas de hardware.

- **Loki**: Agregador de logs especializado en eventos del sistema y Firewalld.

- **Promtail**: Agente de transporte que conecta el systemd-journal de Fedora con Loki.

- **Node-Exporter**: Monitorización de recursos físicos (CPU, RAM, Disco).

- **cAdvisor**: Análisis en tiempo real del consumo de recursos de los contenedores.

## 🔍 Caso de Uso: Identificación y Seguridad

El proyecto permite correlacionar eventos de red con identidades de dispositivos. Durante el desarrollo, se logró identificar dispositivos "fantasma" (como un Samsung Galaxy Watch SM-R870) mediante el análisis de logs de firewall y tablas DHCP, monitorizando su comportamiento de bajo consumo desde el dashboard.

## 🚀 Despliegue Rápido

He incluido scripts de automatización para facilitar el ciclo de vida del stack:

Levantar el entorno:

Abre una terminal y primero da permisos de ejecución a los archivos **setup.sh** y **cleanup.sh**:

```bash
chmod +x scripts/*.sh
```

Levanta el entorno:

```bash
./scripts/setup.sh
```

Limpia el sistema:

```bash
./scripts/cleanup.sh
```

## 📊 Endpoints Disponibles

- **Grafana**: http://localhost:3000 (User: admin / Pass: admin)

- **Prometheus**: http://localhost:9091 (Puerto alternativo para evitar conflictos con Cockpit)

- **cAdvisor**: http://localhost:8080

## 💡 Nota sobre Fedora & Seguridad

Este repositorio está optimizado para **Fedora Linux**, utilizando el etiquetado de volúmenes :Z para compatibilidad con **SELinux** y lectura directa del socket del Journal, garantizando que el monitoreo no comprometa la seguridad del sistema operativo.
