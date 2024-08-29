---
title: Docker HA Windows install
---

On Windows   [Home Assistant](https://www.home-assistant.io/) from Docker Desktop is not supported to open port 8123

### Expose port from CLI

```
docker run -d -p 8123:8123 --privileged --volume "C:\homeassistant:/config" --name homeassistant -e "TZ=Europe/Paris" ghcr.io/home-assistant/home-assistant:stable
```

