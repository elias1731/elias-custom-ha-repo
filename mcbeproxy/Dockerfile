ARG BUILD_FROM=ghcr.io/hassio-addons/base/amd64:10.0.1
FROM ${BUILD_FROM} AS AddonBase

ENV LANG C.UTF-8

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Build BedrockConnect environment

FROM openjdk:11 AS OpenJDK11
RUN mkdir -p /app/bedrockconnect
ADD https://github.com/Pugmatt/BedrockConnect/releases/latest/download/BedrockConnect-1.0-SNAPSHOT.jar /app/bedrockconnect
ADD https://raw.githubusercontent.com/elias1731/elias-custom-ha-repo/main/mcbeproxy/custom/custom_servers.json /app/bedrockconnect
# ADD https://raw.githubusercontent.com/Pugmatt/BedrockConnect/master/docker/custom-servers/custom_servers.json /app/bedrockconnect
EXPOSE 19132/udp

# Add MCXboxBroadcast Stuff

RUN mkdir -p /app/xboxbc
ADD https://github.com/rtm516/app/MCXboxBroadcast/releases/latest/download/app/MCXboxBroadcastStandalone.jar /app/xboxbc

# Run the JARs

WORKDIR /app
CMD ["java", "-Xms512M", "-Xmx512M", "-jar", "bedrockconnct/BedrockConnect-1.0-SNAPSHOT.jar", "nodb=true", "custom_servers=/app/custom_servers.json"]
CMD ["java", "-jar", "xboxbc/MCXboxBroadcastStandalone.jar"]

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Franck Nijhof <frenck@addons.community>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
