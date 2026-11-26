# Canceled and late trains to Uppsala

A [single-file web page](viewer/) that shows arrivals at Uppsala C that are canceled ("Inställt") or running late, using live data from Trafikverket's Open API.

## What it shows

- Canceled arrivals at Uppsala, with the scheduled time struck through
- Late arrivals, with the expected time, the delay at Uppsala, and how late the train is right now (from its last reported stop)
- Refreshes every minute

## Settings

All settings are remembered in your browser.

| Setting | Meaning |
| --- | --- |
| Look ahead | How far ahead to look: 2, 4, 8 or 24 hours |
| Count as late from | Minimum delay to list: 1, 3, 5, 10 or 15 minutes |
| Late measured by | Expected at Uppsala, current delay, or either |
| Only trains that end in Uppsala | Hides trains that continue past Uppsala (on by default) |
| Only SL Pendeltåg | Keeps trains whose product type contains "pendel" (on by default) |

## Setup

1. Get a free API key from [Trafikverket's Open API](https://data.trafikverket.se/): Go to [https://data.trafikverket.se/get-started](https://data.trafikverket.se/get-started), under "Kom igång med API Öppna Data" choose "Registrera ett konto". Then log in to "API Öppna Data". Go back to [https://data.trafikverket.se/get-started](https://data.trafikverket.se/get-started) and choose "Skapa en nyckel". 
2. Open `index.html` in a browser.
3. Paste your key into the page and press **Check now**.

You can also pass the key in the address:

- `index.html#key=YOUR_KEY` (recommended; the part after `#` is never sent to a server)
- `index.html?key=YOUR_KEY` (the key is sent to the host and may appear in its logs)

The page removes the key from the address bar after reading it.

## Notes on the API key

- The key is stored in your browser's `localStorage` on the device you use. It is not in this repository.
- Anyone else who opens the page needs their own key.
- Use a key dedicated to this project, and treat any link that contains it as a secret. If it leaks, revoke it in your Trafikverket account.
- Pages under the same `github.io` account share one `localStorage`, so other pages you host there could read the key.

## Limitations

- The browser calls `api.trafikinfo.trafikverket.se` directly. If the API does not allow requests from your page's origin (CORS), put a small proxy in front of it.
- Delay figures depend on Trafikverket's estimates, which can change as trains run. A train that has not left its first station has no current delay yet.
- The Pendeltåg filter checks the train's product type, not the operator, so other commuter trains labeled "Pendeltåg" may also appear.
