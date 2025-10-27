FROM ghost:5-alpine

# Set working directory
WORKDIR /var/lib/ghost

# Copy custom config
COPY config.production.json .

# Pastikan file dan folder dimiliki user 'node'
RUN chown -R node:node /var/lib/ghost

# Jalankan sebagai user non-root
USER node

# Expose default Ghost port
EXPOSE 2368

#CMD ["node", "current/index.js"]
