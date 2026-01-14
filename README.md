# strava-oauth
Lightweight python server that implements [Strava Oauth Web Flow](http://developers.strava.com/docs/authentication/)

Fork updated to use `fastapi` instead of `responders`.

## Quick start

```bash
git clone https://github.com/sladkovm/strava-oauth.git
cd strava-oauth
```

Setup environment:

```bash
cp .env.example .env
```

Add your Strava app credentials:

```env
# Strava API Credentials (get from https://www.strava.com/settings/api)
STRAVA_CLIENT_ID=your_client_id_here
STRAVA_CLIENT_SECRET=your_client_secret_here
APP_URL=http://localhost
```

Install dependencies:

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Run locally:

```bash
make run
```

Or directly:

```bash
uvicorn api:app --host 0.0.0.0 --port 5042 --reload --ws none
```

Run with Docker:

```bash
make build
```

## Usage

In the web browser go to: *http://127.0.0.1:5042/authorize*

1. You will be redirected to the Strava authorization page
2. After authorization is granted, the browser will display a raw JSON with the authorization tokens

```
Example Response
{
  "token_type": "Bearer",
  "access_token": "987654321234567898765432123456789",
  "athlete": {
    #{summary athlete representation}
  },
  "refresh_token": "1234567898765432112345678987654321",
  "expires_at": 1531378346,
  "state": "https://github.com/sladkovm/strava-oauth"
}
```

3. The output will get saved to `strava_token.json`

## API Endpoints

Endpoint                       |Description              
-------------------------------|-------------------------
GET /                          |Home page with login link
GET /authorize                 |Redirect to Strava login 
GET /authorization_successful  |Exchange code for token  
GET /my_activities             |List last 5 activities   

