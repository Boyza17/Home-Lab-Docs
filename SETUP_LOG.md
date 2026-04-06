## 🔧 Maintenance: Portainer Update
**Task:** Upgrade Portainer Community Edition to the latest version.

### 🚀 Commands Used:
1. `docker stop portainer` & `docker rm portainer` (Clean up old instance).
2. `docker pull portainer/portainer-ce:latest` (Fetch latest security patches).
3. `docker run ... -v portainer_data:/data` (Re-deploy while preserving database).

**Logic:** By mounting the `portainer_data` volume, the configuration, users, and environment settings are persistent across container upgrades.