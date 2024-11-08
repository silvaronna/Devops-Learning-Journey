# Server Performance Stats
A bash script to analyse basic server performance stats.  

## Getting Started
1. **Make a Service File named "server-stats.sh"**
    ```
    sudo nano server-stats.sh
    ```
2. **Insert Configuration Script at the file**
    ```
    #!/bin/bash

 Function to get total CPU usage
get_cpu_usage() {
    echo "Total CPU Usage:"
    mpstat | awk 'NR==4 {printf "CPU Usage: %.2f%\n", 100 - $13}'
    echo
}

 Function to get total memory usage
get_memory_usage() {
    echo "Total Memory Usage:"
    free -h | awk 'NR==2 {printf "Used: %s, Free: %s, Percentage: %.2f%\n", $3, $7, $3/$2*100}'
    echo
}

 Function to get total disk usage
get_disk_usage() {
    echo "Total Disk Usage:"
    df -h | awk '$NF=="/"{printf "Used: %s, Free: %s, Percentage: %.2f%\n", $3, $4, $3/$2*100}'
    echo
}

 Function to get top 5 processes by CPU usage
get_top_cpu_processes() {
    echo "Top 5 Processes by CPU Usage:"
    ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6
    echo
}

 Function to get top 5 processes by memory usage
get_top_memory_processes() {
    echo "Top 5 Processes by Memory Usage:"
    ps -eo pid,comm,%mem --sort=-%mem | head -n 6
    echo
}

 Main script execution
echo "=== Server Performance Stats ==="
get_cpu_usage
get_memory_usage
get_disk_usage
get_top_cpu_processes
get_top_memory_processes
echo "=== End of Stats ==="
    ```

3. **Make the script executable**
    ```
    chmod +x server-stats.sh
    ```
4. **Execute the script**  
    ```
    ./server-stats.sh
    ```
This project is part of [roadmap.sh](https://roadmap.sh/projects/server-stats) DevOps projects.
