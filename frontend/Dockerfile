# build stage
FROM node:18-alpine AS build
WORKDIR /app

# Accept build arguments
ARG VITE_API_URL
ENV VITE_API_URL=$VITE_API_URL

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

# production nginx stage
FROM nginx:stable-alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]


#  docker build -d --build-arg VITE_BACKEND_URL=http://localhost:4000/api/v1 --build-arg VITE_RAZORPAY_KEY=rzp_test_6JJGyNVMuN0u3J -t studynotion-frontend .

# docker run -d -p 3000:80 --name studynotion-frontend studynotion-frontend
