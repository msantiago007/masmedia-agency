# MAS · Netlify Deploy Guide

The `site/` folder is deploy-ready: `index.html`, `thank-you.html`, `sitemap.xml`, `robots.txt`, `netlify.toml`. Follow these steps in order.

## 1. Deploy the site
1. Sign in at app.netlify.com.
2. On the "Sites" tab, drag the entire `site/` folder onto the "deploy manually" drop zone (or use "Add new site" · "Deploy manually").
3. Netlify publishes to a temporary `*.netlify.app` URL. Open it and confirm the page loads.

## 2. Enable the contact form
1. The form already has `data-netlify="true"`, a hidden `form-name` field, and a honeypot, so Netlify detects it automatically on first deploy.
2. Go to Site configuration · Forms and confirm a form named `contact` appears after the first submission. Submit a test message from the live site to register it.
3. Under Forms · Form notifications, add an email notification to msantiago@excelendeavormedia.com (or your preferred inbox).

## 3. Confirm the thank-you redirect
The form posts to `/thank-you.html`, which exists and is set to `noindex`. After a test submit you should land on the "Thank you" page. No extra config needed.

## 4. Connect the domain
1. Site configuration · Domain management · Add a custom domain: enter `masmedia.agency`.
2. Netlify will prompt you to either use Netlify DNS (recommended) or point your registrar's records.
   - Netlify DNS: update the nameservers at your registrar to the four Netlify nameservers shown.
   - External DNS: add an `A` record for the apex to Netlify's load balancer IP and a `CNAME` for `www` to your `*.netlify.app` site, per the values Netlify displays.
3. Set the primary domain to `www.masmedia.agency` so it matches the canonical and OG URLs in the site.
4. Wait for DNS to propagate, then enable HTTPS (Let's Encrypt) under Domain management · HTTPS · "Verify DNS configuration" then "Provision certificate."

## 5. Final live checks
- Click every nav link (Work, Services, Clients, About, Book a consult) and confirm smooth scroll.
- Open several case-study cards and confirm each modal shows Problem / Solution / Results.
- Submit the contact form and confirm the email notification arrives and the thank-you page loads.
- Visit `https://www.masmedia.agency/sitemap.xml` and `/robots.txt` to confirm they serve.

## Image assets to save into `site/assets/`
The page references these files. `Logo.png` is already in place. Save the three generated images (from the chat) into `site/assets/` with these exact lowercase names so the hero and the two photographic bands light up:

- `assets/hero.png` · wide studio/gear shot, used as the hero background
- `assets/vision.png` · eye and violet data, used in the "Story meets systems" band
- `assets/services.png` · cinema lens, used in the "Film & media production" band

If a file is missing the page still renders cleanly (it falls back to the black/violet treatment), so this is non-blocking for deploy. Filenames are case-sensitive on Netlify.

## Follow-up (optional): real client logos and case-study screenshots
The client wall and case studies currently use styled text. The original Wix CDN URLs for the 15 client logos and 11 case-study screenshots are in `Source Archive/02-Case-Studies.md` and `03-Clients-Booking.md` (strip the `/v1/fill/...` suffix for full resolution). Before embedding the client brand marks (Red Bull, Pella, Ping, etc.), confirm which third-party logos you want to display, since these are owned by the respective brands. Once confirmed, download them into `site/assets/` and wire them in.
