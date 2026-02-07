# ---------- BUILD STAGE ----------
FROM node:20-alpine AS build

WORKDIR /app

# copy package files
COPY package*.json ./
RUN npm install

# copy all source
COPY . .

# build react app
RUN npm run build


# ---------- RUNTIME STAGE ----------
FROM nginxinc/nginx-unprivileged:alpine

# copy build files to nginx html folder
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 8080
