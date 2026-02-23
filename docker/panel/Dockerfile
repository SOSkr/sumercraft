

FROM ghcr.io/pterodactyl/panel:v1.12.1

# Copy plugin manager directly to /app
# RUN git clone --depth=1 https://github.com/imTheoDoR/pterodactyl-plugin-manager.git /tmp/plugin && cp -r /tmp/plugin/* /app && rm -rf /tmp/plugin
# Install Blueprint dependencies
RUN apk add --no-cache ca-certificates curl git gnupg unzip wget zip nodejs npm yarn bash

# Download and install Blueprint in /app
RUN wget "$(curl -s https://api.github.com/repos/BlueprintFramework/framework/releases/latest | grep 'browser_download_url' | grep 'release.zip' | cut -d '"' -f 4)" -O release.zip \
	&& unzip -o release.zip \
	&& rm release.zip

# Install Node dependencies
RUN npm i -g yarn && yarn install

# Configure Blueprint for nginx user
RUN echo 'WEBUSER="nginx";\nOWNERSHIP="nginx:nginx";\nUSERSHELL="/bin/sh";' > /app/.blueprintrc

# Make blueprint.sh executable and run it with bash
RUN chmod +x /app/blueprint.sh && bash /app/blueprint.sh
