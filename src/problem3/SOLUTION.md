Provide your solution here:

Issue: Log growth fill up disk space
  Symptoms:
    Disk usage reach 99%
    Nginx continues running but may slow or fail under high traffic
    Logs may be bloating due to misconfig
  Troubleshoot:
    Verify disk usage.
    Determine how nginx is running: directly, containerized / dockerized.
    Identify large files or directories
    Inspect log files
    Check housekeeping for service nginx
  Cause: 
    Unmanaged log files growing indefinitely.
    Misconfigured log rotation settings causing accumulation
    High traffic generating excessive logs.
    Lot of errors.
  Impact:
    Application / Service failures or crash the VM
    Nginx may stop responding correctly if log cannot be written.
    Loss of incoming traffic due to service disruption.
  Recovery steps:
    Manually clear log, use truncate to clear logs without deleting the file structure.
    Make sure log is mounted correctly to host (in case nginx is containerized / dockerized).
    Review log file configuration in nginx config.
    Make sure log rotation is mapping correct folder and working as expected, adjust rotation limits and compression.
    Restart nginx service / container / pods / docker service



Issue: Unexpected disk usage
  Symptoms:
    Disk usage spikes despite proper log rotation.
    Nginx performance drops unexpectedly 
  Troubleshoot:
    Check nginx cache.
    Identify large or unnecessary temporary files.
    Check nginx config proxy buffering
  Cause: 
    Large cache files accumulating beyond intended limits.
    Temporary files lingering and not being cleared
  Impact:
    Disk space exhaustion may cause NGINX failures
    Traffic could be interrupted due to unavailable disk space.
    Performance degradation in response time and throughput.
  Recovery steps:
    Manually clear cache.
    Adjust cache policy in nginx config.
    Restart nginx service.



Issue: User files
  Symtons:
    Large, unexpected storage consumption in a user-accessible directory
    High disk usage without excessive log growth or cache accumulation
  Troubleshoot:
    Check location of large files.
  Cause: 
    Users conducting tests and forgetting to delete files.
    Accidental uploads consuming significant space
  Impact:
    Potential NGINX load balancer issues if upstream services rely on free space
    Degraded performance affecting request handling.
    Service failure.
  Recovery steps:
    Cleanup unwanted files 
