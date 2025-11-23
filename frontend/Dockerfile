# ------------------- Stage 1: Build Stage ------------------------------
    FROM node:21 AS build

    WORKDIR /app
    
    COPY package*.json ./
    RUN npm install
    
    COPY . .
    RUN npm run build     # <-- builds the dist folder
    
    # ------------------- Stage 2: Serve with Nginx -------------------------
    FROM nginx:alpine
    
    # Copy the built frontend files to nginx www folder
    COPY --from=build /app/dist /usr/share/nginx/html
    
    # Replace default Nginx config (optional but recommended)
    COPY nginx.conf /etc/nginx/conf.d/default.conf
    
    EXPOSE 80
    
    CMD ["nginx", "-g", "daemon off;"]
    