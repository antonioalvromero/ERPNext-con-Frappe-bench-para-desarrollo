# ERPNext-con-Frappe-bench-para-desarrollo

# 🚀 Guía de instalación de ERPNext con Docker

Este repositorio documenta los pasos necesarios para montar **ERPNext (v15)** utilizando **Docker** y **Frappe Bench**.  
La guía está basada en la experiencia práctica de despliegue y configuración de módulos clave como **ERPNext**, **Payments**, **Webshop**, **Helpdesk** y **Chat**.

---

## 📋 Prerrequisitos

1. **Instalar Ubuntu**
   - Descargar desde Microsoft Store: **Ubuntu 24.04.1 LTS**

2. **Configurar Docker Desktop**
   - Ir a: `Docker > Configuración > Resources > WSL integration`
   - Activar ambas opciones.


---

## ⚙️ Instalación inicial

```bash
git clone https://github.com/frappe/frappe_docker
cd frappe_docker/devcontainer-example

docker compose up -d
docker exec -it devcontainer-example-frappe-1 bash
```

Dentro del contenedor:
```bash
apt update
apt install redis-server -y
```
---
## 🏗️ Configuración de Frappe Bench

```bash
bench init frappe-bench --frappe-branch version-15
cd frappe-bench

```

Editar el archivo sites/common_site_config.json y agregar:

```bash
{
  "db_host": "[IP DEL SERVIDOR MARIADB]",
  "db_port": 3306,
  "db_name": "rrtechnology.local",
  "db_password": "123",
  "db_type": "mariadb",
  "db_user": "root"
}


```
Crear un nuevo sitio:
```bash
bench new-site rrtechnology.local

```
En caso de necesitar eliminarlo:
```bash
bench drop-site rrtechnology.local --force


```
---

# 📦 Instalación de aplicaciones
##ERPNext y módulos principales

```bash
bench get-app erpnext --branch version-15
bench --site rrtechnology.local install-app erpnext

bench get-app payments --branch version-15
bench --site rrtechnology.local install-app payments

bench get-app webshop --branch version-15
bench --site rrtechnology.local install-app webshop

```
Esto habilita:

Página de productos

Carrito de compras

Wishlist

Reseñas

Navegación por categorías

📖 Documentación oficial de e-commerce

---
## Otros módulos útiles
### Helpdesk
```bash
bench get-app helpdesk --branch main
bench --site rrtechnology.local install-app helpdesk


```
Gestión de tickets, SLA, asignaciones y respuestas automáticas

Integración con correo electrónico y CRM

### Chat
```bash
bench get-app chat --branch main
bench --site rrtechnology.local install-app chat

```
Mensajería interna en tiempo real

Chats entre usuarios y grupos

Integración con menciones y comentarios

---

# ▶️ Ejecución
Desde /frappe-bench:
```bash
bench use rrtechnology.local
bench start

```
---

# 🛒 Configuración del Webshop

1. Ir a Website Settings, configurar y guardar.

2.Crear productos en Item List:

-Seleccionar Stock Information All Warehouses

-Publicar desde el Action del producto

3.Añadir stock:

-Stock > Stock Entry > Add Stock Entry

4.Crear proveedor:

Buying > Supplier

5.Crear orden de compra:

Buying > Purchase Order → Submit

6.Registrar recepción:

Purchase Receipt → Submit

7.Verificar en Stock Balance
