# misp-ioc-extractor
Extracts IOCs from MISP and uploads the IOCs for IPs, domains, and file hashes to an AWS S3 bucket.

# Prerequisites
1. An active instance of MISP. For installation instructions, reference: https://misp.github.io/MISP/
2. An AWS subscription & pubically accessible S3 bucket.
3. Install AWS SDK
```
pip install boto3
```

# Installation
## Set environment variables

```
export MISP_URL='https://your-misp-instance.com'
export MISP_API_KEY='YOUR_API_KEY'
export AWS_ACCESS_KEY_ID='AWS_ACCESS_KEY_ID'
export AWS_SECRET_ACCESS_KEY='AWS_SECRET_ACCESS_KEY'
```



## Enable as service
```
nano /etc/systemd/system/fetch-misp-ioc.service
```
```
[Unit]
Description=My MISP polling service
After=network.target

[Service]
Type=simple
User=your-user
Environment="MISP_URL=https://your-misp-instance.com"
Environment="MISP_API_KEY=YOUR_API_KEY"
Environment="AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY"
Environment="AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY"
ExecStart=/usr/bin/python /path/to/your/script.py

Restart=on-failure
RestartSec=30s

[Install]
WantedBy=multi-user.target
```
# R```eload systemd
