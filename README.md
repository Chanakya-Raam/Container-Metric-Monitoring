# Docker Containers Metrics Monitoring In Grafana Using Cadvisors and Prometheus

This service is set up to monitor Docker container metrics such as CPU usage, RAM usage, and other statistics. It uses Cadvisor and Prometheus to export this data, which can then be viewed directly in a Grafana dashboard. Docker Compose is used to run all these services together.
## Setup and Usage

Follow the steps below to set up and use the container monitoring system:

![image](https://github.com/Chanakya-Raam/Container-Metric-Monitoring/assets/122670542/22735805-7cd8-4c99-846d-d581cb3971a1)



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
### Grafana Credentials
Use the default credentials to log in:

Username: `admin`
Password: `admin`

### 4. Access Cadvisor and Prometheus 

Check the Services by running it on localhost

* Cadvisor `localhost:8080` (Port number can vary , check `docker-compose.yml`)
  
  ![image](https://github.com/Chanakya-Raam/Container-Metric-Monitoring/assets/122670542/b122d1f4-913a-4191-857f-86698abc32c6)


* Prometheus `localhost:9090` and `localhost:9090/metrics`  which shows the metrics in Unstructured form like this
```bash
# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 5.5865e-05
go_gc_duration_seconds{quantile="0.25"} 0.000271015
go_gc_duration_seconds{quantile="0.5"} 0.000496259
go_gc_duration_seconds{quantile="0.75"} 0.000947251
go_gc_duration_seconds{quantile="1"} 0.094369482
go_gc_duration_seconds_sum 2.290822738
go_gc_duration_seconds_count 1420
# HELP go_goroutines Number of goroutines that currently exist.
# TYPE go_goroutines gauge
go_goroutines 39
# HELP go_info Information about the Go environment.
# TYPE go_info gauge
go_info{version="go1.22.2"} 1
# HELP go_memstats_alloc_bytes Number of bytes allocated and still in use.
# TYPE go_memstats_alloc_bytes gauge
go_memstats_alloc_bytes 5.5855856e+07
# HELP go_memstats_alloc_bytes_total Total number of bytes allocated, even if freed.
# TYPE go_memstats_alloc_bytes_total counter
go_memstats_alloc_bytes_total 2.3186695312e+10
# HELP go_memstats_buck_hash_sys_bytes Number of bytes used by the profiling bucket hash table.
# TYPE go_memstats_buck_hash_sys_bytes gauge
go_memstats_buck_hash_sys_bytes 1.773819e+06
# HELP go_memstats_frees_total Total number of frees.
# TYPE go_memstats_frees_total counter
go_memstats_frees_total 3.7271982e+07
```

### 5. Add Dashboard:
* Navigate to the dashboards section in Grafana.
* `Dashboard > new > import >` and `upload json`
* (json is `dashboard.json` in the repo)

* Use the dashboard template provided in the repository (dashboard.json). This template is pre-configured with queries to display metrics of the running containers individually from `google/cadvisor` and `Prometheus` running in Docker .

### 6. Ready to Monitor the Container Statistics:
* Your setup is now complete. You should be able to monitor the Docker container metrics of individual containers directly from the Grafana dashboard.
