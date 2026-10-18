# EC2 Backend

Application directory: `/home/ssm-user/contact-api/`

Main files: `app.py`, `.env`, and a Python virtual environment.

Install:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Run with Gunicorn:

```bash
gunicorn --workers 3 --bind 0.0.0.0:5000 app:app
```

Health test:

```bash
curl http://127.0.0.1:5000/health
```

Expected HTTP 200 and `{"status":"healthy"}`.

The ALB uses this endpoint as its health check. Two app instances provide redundancy.
