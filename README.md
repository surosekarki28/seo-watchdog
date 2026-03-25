# SEO Watchdog

A Django webapp that monitors your website's keyword rankings via Google Search Console, alerts you to drops/rises, and visualizes history with Chart.js.

## Setup

### 1. Install dependencies
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 2. Configure environment
```bash
cp .env.example .env
# Edit .env with your values
```

### 3. Google Cloud Console setup
1. Go to https://console.cloud.google.com
2. Create a new project
3. Enable **Google Search Console API**
4. Go to **Credentials** → Create **OAuth 2.0 Client ID** (Web application)
5. Add Authorized redirect URI: `http://localhost:8000/properties/auth/callback/`
6. Copy Client ID and Client Secret into your `.env`

### 4. Database setup
```bash
python manage.py migrate
python manage.py createsuperuser
```

### 5. Run the server
```bash
python manage.py runserver
```

Visit http://localhost:8000 and log in.

## Usage

1. **Connect a property** → Properties → Connect Google Search Console
2. **Add keywords** → Keywords → Add Keyword (select your property)
3. **Set alert rules** → Click any keyword → Add Rule (e.g. drop > 5 positions)
4. **Fetch data** → Click "Fetch Now" on any keyword detail page
5. **View alerts** → Bell icon in navbar shows unread alert count
6. **Compare** → Compare tab to see two properties side by side

## Alerts

Configure in Profile Settings:
- **Email**: set `EMAIL_HOST_USER` / `EMAIL_HOST_PASSWORD` in `.env`
- **Slack**: paste your Slack Incoming Webhook URL in Profile Settings

## Scheduler

Rankings are fetched automatically daily at **06:00 UTC**. GSC data has a ~3 day delay, so today's fetch covers data up to 3 days ago. You can also trigger manual fetches per keyword.
