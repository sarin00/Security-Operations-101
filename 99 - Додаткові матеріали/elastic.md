$ProgressPreference = 'SilentlyContinue'  
Invoke-WebRequest -Uri https://artifacts.elastic.co/downloads/beats/elastic-agent/elastic-agent-8.15.2-windows-x86_64.zip -OutFile elastic-agent-8.15.2-windows-x86_64.zip  
Expand-Archive .\elastic-agent-8.15.2-windows-x86_64.zip -DestinationPath .  
cd elastic-agent-8.15.2-windows-x86_64  
.\elastic-agent.exe install --url=https://0211b21a497d4f338b6e01a6f0023cf7.fleet.us-central1.gcp.cloud.es.io:443 --enrollment-token=
