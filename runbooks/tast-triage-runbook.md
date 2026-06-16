# DAST Troubleshooting Playbook

1. Check operational status of target system daemon:
   `sudo systemctl status gunicorn.service`

2. Clear frozen application sockets:
   `sudo systemctl restart gunicorn.service`

3. Run terminal loopback health diagnostics:
   `curl -I http://localhost:8000`
