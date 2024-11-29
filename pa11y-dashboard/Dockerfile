# Use Node.js 16 as the base image
FROM node:16

# Install necessary system dependencies for Chromium
RUN apt-get update && apt-get install -y \
  libnss3 \
  libatk1.0-0 \
  libatk-bridge2.0-0 \
  libcups2 \
  libdbus-1-3 \
  libxcomposite1 \
  libxrandr2 \
  libxdamage1 \
  libgbm1 \
  libpango-1.0-0 \
  libasound2 \
  libpangocairo-1.0-0 \
  libxshmfence1 \
  libgtk-3-0 \
  --no-install-recommends && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# Create a non-root user called "puppeteer"
RUN useradd -ms /bin/bash puppeteer

# Set the working directory and ensure the app files are owned by "puppeteer"
WORKDIR /app
COPY --chown=puppeteer:puppeteer package*.json ./
RUN npm install
COPY --chown=puppeteer:puppeteer . .

# Switch to the non-root user
USER puppeteer

# Expose the port used by the application
EXPOSE 8080

# Start the application
CMD ["npm", "start"]
