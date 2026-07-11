# Casa Silvas — Property Site

Public-facing listing page for Casa Silvas, a private guest suite in Tucson, AZ, managed by AI&I.

## Structure

```
index.html      → the entire site (single file, no build step)
images/          → all property photos, referenced by index.html via relative paths
```

## Deploying

This is a static site — no build step, no framework, no dependencies.

**Vercel:**
1. Import this repo in Vercel.
2. Framework Preset: **Other**
3. Build Command: *(leave blank)*
4. Output Directory: `.`
5. Deploy.

## Booking form

The "Request to Book" form on the site POSTs to a Supabase Edge Function
(`casa-silvas-book`) in the `ai-and-i` Supabase project, which saves the
request to the `casa_silvas_bookings` table and sends email notifications
via Resend.

To enable email notifications, set these secrets on the Edge Function
(Supabase Dashboard → Edge Functions → casa-silvas-book → Secrets):

- `RESEND_API_KEY`
- `NOTIFY_EMAIL`
- `FROM_EMAIL` *(optional — falls back to Resend's shared test address)*

Without those secrets, form submissions still save to the database, they
just won't trigger emails yet.

## Images

All photos are `.webp`, pre-compressed for web (folder totals ~3MB).
Naming convention: `room-##[-detail].webp`, e.g. `kitchen-02-range.webp`.
