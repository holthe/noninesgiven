# No Nines Given

**Downtime as a Service.** Guaranteed 0.000% uptime, or your money back.

This repository contains the public marketing site for No Nines Given
(noninesgiven.com), the industry's first and only provider of contractually
guaranteed unavailability.

## The Product

Every other vendor in this category sells you availability and then quietly
fails to deliver it. We took the opposite position. We sell you unavailability
and we deliver it completely, on every request, without exception.

Key differentiators:

- **0.000% uptime SLA.** Not "three nines." Not "five nines." No nines given.
- **Deterministic outcomes.** Our response is identical under all load
  conditions, which makes capacity planning trivial.
- **Zero attack surface at the application layer.** There is no application
  layer.
- **No incident reviews.** An incident requires a deviation from expected
  behavior. We have never deviated.
- **Predictable cost.** Compute spend is flat because nothing computes.

Our uptime is currently 0.000% and has been 0.000% since inception. We consider
this our strongest operational record in the sector.

## Architecture

The site is a static, zero-build, zero-dependency deployment. Two HTML files,
one font directory. There is no framework, no bundler, no package.json, and no
build step. This is deliberate and is not an oversight to be corrected.

```
index.html      the site
404.html        catch-all, served automatically by Cloudflare Pages
fonts/          self-hosted woff2 files (latin subset)
wrangler.toml   Cloudflare Pages configuration
```

Fonts are self-hosted. The site makes zero requests to any external domain,
which means our downtime is entirely our own achievement and is not dependent
on a third party CDN. We are not willing to outsource our core competency.

## Deploying

### Option A: Wrangler CLI

Requires the Cloudflare Wrangler CLI and an authenticated account.

```sh
npm install -g wrangler
wrangler login

# Create the Pages project once.
wrangler pages project create noninesgiven --production-branch main

# Deploy.
wrangler pages deploy .
```

Subsequent deploys are just `wrangler pages deploy .`.

### Option B: Cloudflare dashboard (Git integration)

1. Push this repository to GitHub.
2. Open the Cloudflare dashboard and go to **Workers & Pages**.
3. Select **Create**, then the **Pages** tab, then **Connect to Git**.
4. Authorize GitHub and select the `noninesgiven` repository.
5. Configure the build settings exactly as follows:
   - **Project name:** `noninesgiven`
   - **Production branch:** `main`
   - **Framework preset:** None
   - **Build command:** leave empty
   - **Build output directory:** `/`
6. Select **Save and Deploy**.

There is no build command because there is nothing to build. Any value entered
here will make the deployment worse.

### Custom domain

After the first successful deploy:

1. Open the `noninesgiven` project in the Cloudflare dashboard.
2. Go to **Custom domains**, then **Set up a custom domain**.
3. Enter `noninesgiven.com` and select **Continue**.
4. If the zone is already on Cloudflare, the required CNAME record is created
   for you. Confirm and wait for the certificate to be issued.
5. Repeat for `www.noninesgiven.com` if you want the apex and www to both
   resolve.

Certificate issuance usually completes in a few minutes. This is the longest
any part of this system will ever be doing work.

## Local development

```sh
python3 -m http.server 8000
```

Then open `http://localhost:8000`. A local server is required rather than
opening the file directly, because the font paths are root absolute.

## Support

Support is available 0 hours per day, 0 days per week. Response times are not
measured because no responses are issued. Customers reporting that the service
is unavailable will be thanked for confirming that the SLA is being met.

## Status page

The status page is part of the service and is therefore also down. This is
consistent by design.

## License

The site is a parody. IBM Plex and Archivo are licensed under the SIL Open Font
License 1.1 and are redistributed here under those terms.
