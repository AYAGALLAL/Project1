#!/bin/bash

# CPU usage
echo "CPU usage"
cpu_usage=$(top -bn1 | grep "CPU(s)" | awk '{usage=100-$8} END {print usage "%"}')

# memory usage
echo "memory usage"
memory_usage=$(free -m | grep "MEM(s)" | awk '/^MEM:/ {printf "used: %dMB, free: %dMB (%.2f%%)\n", $3, $4, $3/$2*100}')

# disk usage
echo "disk usage"
disk_usage=$(df -h --total | awk '/^total/ {printf "used: %sMB, free: %sMB (%s)\n", $3, $4, $5}')

# Top 5 processes by CPU usage
echo "Top 5 processes by CPU usage"
ps -eo pid,comm,%cpu --sort=-%cpu | head -n 6 

# Top 5 processes by memory usage
echo "Top 5 processes by memory usage"
ps -eo pid,comm,%mem --sort=-%mem | head -n 6 

