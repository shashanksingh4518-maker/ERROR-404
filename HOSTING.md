# Hosting Guide – One Platform Complete Healthcare

## OTP (SMS) setup (Twilio)

1. **Twilio account**: Sign up at [twilio.com](https://www.twilio.com).
2. **Verify Service**: In [Twilio Console](https://console.twilio.com) go to **Verify** → **Services** → create a new service. Copy the **Service SID** (starts with `VA...`).
3. **Credentials**: From Console → **Account** copy **Account SID** and **Auth Token**.
4. **Local**: Copy `.env.example` to `.env` and set:
   - `TWILIO_ACCOUNT_SID`
   - `TWILIO_AUTH_TOKEN`
   - `TWILIO_VERIFY_SERVICE_SID`
5. Run: `npm install` then `npm start`. Open `http://localhost:3000/login.html`. Use **Send OTP** with a 10-digit mobile (for trial, use your Twilio-verified number).

---

## Deploy (host) the app

### Option A: Render (recommended)

1. Push your code to a **GitHub** repo.
2. Go to [render.com](https://render.com) → **New** → **Web Service**.
3. Connect the repo. Set:
   - **Build**: `npm install`
   - **Start**: `npm start`
   - **Environment**: Add variables:
     - `TWILIO_ACCOUNT_SID`
     - `TWILIO_AUTH_TOKEN`
     - `TWILIO_VERIFY_SERVICE_SID`
4. Deploy. Your app will run at `https://<your-app>.onrender.com`. Use **Login with OTP**; OTP will be sent to the entered phone via SMS.

### Option B: Railway

1. Push code to **GitHub**.
2. Go to [railway.app](https://railway.app) → **New Project** → **Deploy from GitHub**.
3. Select repo. Add the same **Twilio env variables** in **Variables**.
4. Set start command: `npm start`. Deploy. Use the generated URL.

### Option C: Other Node hosts

- **Heroku**, **Fly.io**, **Cyclic**: Same idea – set `PORT` (they often set it automatically) and the three Twilio env variables, then `npm start`.

---

## Notes

- **Twilio trial**: SMS works only to numbers you verify in Twilio Console. For any Indian number, upgrade the account.
- **Indian numbers**: Use 10-digit mobile; the server adds `+91` for Twilio.
- **HTTPS**: On Render/Railway the site is HTTPS, so `location.origin` is correct for API calls.
