# Docker Containers Metrics Monitoring In Grafana Using Cadvisors and Prometheus

This service is set up to monitor Docker container metrics such as CPU usage, RAM usage, and other statistics. It uses Cadvisor and Prometheus to export this data, which can then be viewed directly in a Grafana dashboard. Docker Compose is used to run all these services together.
## Setup and Usage

Follow the steps below to set up and use the container monitoring system:


### 1. Install Docker and Docker-compose installed in the system  
```bash
sudo apt-get update && \
sudo apt-get install -y ca-certificates curl gnupg lsb-release && \
sudo mkdir -p /etc/apt/keyrings && \
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && \
sudo apt-get update && \
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin && \
sudo docker run hello-world && \
docker compose version
```

### 2. Clone the Repository

Clone the repository and start the services by running the following command:

```bash
git clone <repository_url>
```
```bash
cd <repository_directory>
```
###  Make sure you check your port numbers in docker-compose.yml file to avoid conflict 
```bash
docker-compose up -d
```
or 
```bash
docker compose up -d
```

### 3. Access Grafana
Open your web browser and navigate to:
```bash
http://localhost:3000
```
### 4. Grafana Credentials
Use the default credentials to log in:

Username: `admin`
Password: `admin`

### 5. Add Dashboard:
* Navigate to the dashboards section in Grafana.
* `Dashboard > new > import >` and `upload json`    (json is `dashboard.json` in the repo)

* Use the dashboard template provided in the repository (dashboard.json). This template is pre-configured with queries to display metrics of the running containers individually from `google/cadvisor` and `Prometheus` running in Docker .

### 6. Ready to Monitor the Container Statistics:
* Your setup is now complete. You should be able to monitor the Docker container metrics of individual containers directly from the Grafana dashboard.
