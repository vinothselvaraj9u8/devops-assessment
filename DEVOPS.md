1. Project Overview
Django Backend

React Frontend

Dockerized using multi-stage builds

2. Local Setup
docker compose up --build


Ports:

Frontend → 3000

Backend → 8000

3. CI/CD

GitHub Actions builds images

Pushes to DockerHub automatically on main branch push

4. Environment Variables

DEBUG

VITE_API_URL

5. Troubleshooting (Important)

Example:

Issue: Nginx permission denied when running non-root

Fix: Switched to nginxinc/nginx-unprivileged image.

6. Screenshot

Add screenshot of:

Frontend running in browser

Backend API working

## Infrastructure as Code
A basic Terraform configuration is included in the `terraform/` folder
to demonstrate VM provisioning knowledge. Not executed due to
account limitations.


## Troubleshooting

### Issue 1 – Nginx Permission Denied
- Error: mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)
- Fix: Used `nginxinc/nginx-unprivileged` image and changed frontend port to 8080.

### Issue 2 – SQLite Database Error
- Error: sqlite3.OperationalError: unable to open database file
- Fix: Changed database path to `/data/db.sqlite3`, added Docker volume, and created writable /data folder in Dockerfile.


