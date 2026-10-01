<<<<<<< HEAD
# Cyber Entertainment — website + admin panel

Zero dependencies. Needs only **Node.js 18+** (no `npm install`).

## Run
    node server.js          # http://localhost:3000
First start prints your admin password once. Log in at **/admin**, then change it under *Account*.
To choose your own: `ADMIN_PASSWORD='your-long-password' node server.js` (first run only).

## What the admin controls
- **Bookings** — every form submission lands here (status, notes, delete, CSV export). Clients still get sent to WhatsApp too.
- **Gear** — add/edit/hide hire items and prices; updates the public site instantly.
- **Settings** — tagline, phone, WhatsApp, email, address, hours, social links.

## Deploy on a VPS (Ubuntu)
    sudo apt install nodejs nginx        # Node 18+ (use NodeSource if older)
    npm i -g pm2 && pm2 start server.js --name cyber && pm2 save && pm2 startup
nginx site (then `certbot --nginx -d yourdomain.com` for free HTTPS):

    server { server_name yourdomain.com; location / { proxy_pass http://127.0.0.1:3000;
      client_max_body_size 300m; proxy_set_header X-Forwarded-For $remote_addr; proxy_set_header X-Forwarded-Proto $scheme; } }

Set `COOKIE_SECURE=1` once HTTPS is on. Any Node host (Render, Railway, cPanel "Setup Node.js App") also works: start command `node server.js`.

## Mixtapes
Admin > Mixtapes: upload mp3/m4a/aac/wav/ogg per DJ (max 300 MB each; change with `MAX_UPLOAD_MB`), or paste a direct audio link. Visitors stream and download from each DJ's sector. Behind nginx keep `client_max_body_size` above your largest file.

## Store
Public at **/store/** (also in the main nav and on each DJ card). Every DJ gets a profile page with their mixtapes and T-shirts. Visitors add tees to a cart, then checkout sends the order to WhatsApp **and** saves it under Admin > Bookings as *Store Order*. No online payment — you confirm and collect payment (e.g. mobile money) yourself.
Admin > **DJs**: bio, genres, Instagram, photo upload. Admin > **T-shirts**: per-DJ name, price (UGX), sizes, image upload. Images are max 8 MB (jpg/png/webp).

## Events
Admin > **Events**: add each upcoming night with name, date, time, venue, line-up, entry price, an optional ticket link and a flyer (upload or link). They appear in the **Upcoming Events** section of the home page (nav: *Events*), soonest first. Leave the date empty to show *Date to be announced* while you are still planning. Status can be set to Sold out, Postponed or Cancelled and the card updates automatically. Events drop off the site the day after their date (they stay in the admin so you can use ⧉ Duplicate for recurring nights). With no ticket link the button opens WhatsApp with the event name pre-filled. Untick *Available* to keep an event as a hidden draft.

## Data & backups
Everything lives in `data/` — back up `data/db.json` **and** `data/media/` (uploaded mixtapes). Never put it in `public/`.

## Security notes
Passwords are scrypt-hashed; login is rate-limited; sessions are HttpOnly + SameSite=Strict; booking form has a honeypot and rate limit; `/admin` and `/api` are excluded from search engines.

## Still yours to do
Replace the stock photography with real photos of your DJs and events (DJ photos can be uploaded in Admin > DJs; hero/gallery images are in `public/index.html`), add real gear descriptions and prices in Admin > Gear, and add a `sitemap.xml` with your domain.

## Visual refresh
The public site now includes local SVG artwork under `public/assets/` for the logo, hero, studio, DJ Academy and gear-hire sections. The refresh removes the previous remote logo dependency and improves responsive presentation without changing the existing admin/API architecture.

## Photography
The public site now includes a visual gallery and photography sourced from Pexels free-to-use listings. The gallery credits the photographers where known. Images are loaded from the Pexels CDN so the ZIP stays lightweight.
=======
# Cyber-Entertainment-Web
Review Web
>>>>>>> bca99a0d39122c43f0920a4983b7ce8780f7cd68
