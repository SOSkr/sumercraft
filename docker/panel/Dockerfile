

FROM ghcr.io/pterodactyl/panel:v1.12.1

# Copy plugin manager directly to /app
# RUN git clone --depth=1 https://github.com/imTheoDoR/pterodactyl-plugin-manager.git /tmp/plugin && cp -r /tmp/plugin/* /app && rm -rf /tmp/plugin
# Install Blueprint dependencies
RUN apk add --no-cache ca-certificates curl git gnupg unzip wget zip nodejs npm yarn bash ncurses icu-libs musl-locales musl-locales-lang libc6-compat

# Set UTF-8 locale environment
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
RUN echo "export LANG=en_US.UTF-8" >> /etc/profile \
	&& echo "export LC_ALL=en_US.UTF-8" >> /etc/profile

# Download and install Blueprint in /app
RUN wget "$(curl -s https://api.github.com/repos/BlueprintFramework/framework/releases/latest | grep 'browser_download_url' | grep 'release.zip' | cut -d '"' -f 4)" -O release.zip \
	&& unzip -o release.zip \
	&& rm release.zip


# Create .blueprintrc with nginx configuration before running Blueprint
RUN echo 'WEBUSER="nginx";\nOWNERSHIP="nginx:nginx";\nUSERSHELL="/bin/sh";\nPERMISSIONS="u=rwX,g=rX,o=rX";' > /app/.blueprintrc

# Install Node dependencies
RUN npm i -g yarn && yarn install

# Make blueprint.sh executable and run it with bash
RUN chmod +x /app/blueprint.sh && bash /app/blueprint.sh

# Opcional: fuerza permisos correctos al final
RUN chown -R nginx:nginx /app && \
	find /app -type d -exec chmod 755 {} \; && \
	find /app -type f -exec chmod 644 {} \; && \
	find /app -type f -name "*.sh" -exec chmod 755 {} \;
