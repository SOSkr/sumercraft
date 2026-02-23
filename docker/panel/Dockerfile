FROM ghcr.io/pterodactyl/panel:v1.12.1

# Install Blueprint and system dependencies
RUN apk add --no-cache ca-certificates curl git gnupg unzip wget zip nodejs npm yarn bash ncurses icu-libs musl-locales musl-locales-lang libc6-compat

# Set UTF-8 locale environment for proper encoding
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
RUN echo "export LANG=en_US.UTF-8" >> /etc/profile \
	&& echo "export LC_ALL=en_US.UTF-8" >> /etc/profile

# Download and install Blueprint in /app
RUN wget "$(curl -s https://api.github.com/repos/BlueprintFramework/framework/releases/latest | grep 'browser_download_url' | grep 'release.zip' | cut -d '"' -f 4)" -O release.zip \
	&& unzip -o release.zip \
	&& rm release.zip

# # Install Node.js dependencies for Blueprint
# RUN npm i -g yarn && yarn install

# # Make blueprint.sh executable and run it with bash
# RUN chmod +x /app/blueprint.sh && bash /app/blueprint.sh

# # Copy custom entrypoint script to container root
# COPY docker/panel/scripts/entrypoint.sh /entrypoint.sh

# # Make entrypoint script executable
# RUN chmod +x /entrypoint.sh

# # Use custom entrypoint to ensure runtime configuration and permissions
# ENTRYPOINT ["/entrypoint.sh"]
