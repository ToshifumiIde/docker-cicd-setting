FROM node:18 AS base
CMD [ "bash" ]

# Build
FROM base AS test-and-build
WORKDIR /workspace
COPY . .
ARG REACT_APP_API_SERVER
RUN npm ci && npm run test && npm run build

# Hosting in nginx
FROM nginx:latest AS production
COPY --from=test-and-build /workspace/build /var/www
COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf