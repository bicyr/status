# status.bicyr.com

Bicyr's status page. It is one static file on GitHub Pages, served from GitHub's
own addresses and never through Cloudflare, so it stays reachable when the
platform is down, and when Cloudflare is. The design is **2.2.6 Disaster Recovery
& Business Continuity**, *The One Vendor on the Public Path*; the build is
[bicyr/.github#215](https://github.com/bicyr/.github/issues/215).

## Declaring or updating an incident

1. Edit `index.html`: the state line, the *Last updated* time (UTC, read from a
   clock), and an entry under *Incident history*.
2. Commit and push to `main`. GitHub Pages publishes it within a minute or two.

There is no build step, no dependency and no workflow, on purpose: the page has to
be updatable from the founder's machine when everything else is down.

## What must stay true

- `CNAME` holds `status.bicyr.com`. Removing it releases the custom domain.
- The DNS record is a **DNS-only** CNAME, `status` → `bicyr.github.io`, with a
  one-day TTL. It is described in `infra/cloudflare` in `bicyr/.github`. Proxying
  it through Cloudflare would put the page on the platform it exists to outlive.
- The address is printed where nobody has to look it up on a platform that is
  down: the run-of-show sheet and the tenant-facing statement (2.2.6).
