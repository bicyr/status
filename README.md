# [Bicyr status](https://status.bicyr.com): <!--live status--> **🟩 All systems operational**

<!--start: status pages-->
<!--end: status pages-->

## About

This repository is Bicyr's status page at **https://status.bicyr.com**. It is
served by GitHub Pages from GitHub's own addresses and never through
Cloudflare, so it stays reachable when the platform is down, and when
Cloudflare is. The design is **2.2.6 Disaster Recovery & Business
Continuity**, *The One Vendor on the Public Path*; the tooling is
decision OD-412, installed
by [bicyr/.github#620](https://github.com/bicyr/.github/issues/620).

The checks and history come from [Upptime](https://github.com/upptime/upptime)
(`upptime/uptime-monitor` v1.44.1): GitHub Actions checks each production host
every five minutes, commits the result here, and opens an issue labelled
`status` and the site's slug when one goes down. The summary above is
rewritten by Upptime; edit outside the markers only.

**Upptime pages nobody.** It is never on the paging path (OD-412 ruling 3): no
notification is configured, and the workflows hand the monitor no repository
secret, so adding one cannot turn a notification on.

### Posting an incident

An incident is an issue with the `status` label; the page lists every open one
as a current incident and every closed one in the history.

- Upptime opens and closes its own, labelled `status` plus a site slug
  (`bicyr-com`, `ami`, `cangor`).
- The Operations Hub opens its own with `status` plus the hub's label and **no
  site slug**, so Upptime never finds and never closes them. The hub's label
  must never equal a site slug, and a hub incident must never carry
  `maintenance`: Upptime closes a `maintenance` issue once its window ends.
- By hand, when everything else is down: open an issue here with the `status`
  label, update it with comments, close it when it is over.

### What must stay true

- `status-website.cname` in `.upptimerc.yml` is `status.bicyr.com`; the site
  build writes it into the published `CNAME`.
- The DNS record is a **DNS-only** CNAME, `status` → `bicyr.github.io`, managed
  in Pulumi from `bicyr/.github`. Proxying it through Cloudflare would put the
  page on the platform it exists to outlive.
- The workflows are maintained by hand. The template's self-update
  (`update-template.yml`, `updates.yml`, and the "Update template" step in
  `setup.yml`) is removed: it would regenerate the workflows from upstream and
  undo their pins and permissions.
- The address is printed where nobody has to look it up on a platform that is
  down: the run-of-show sheet and the tenant-facing statement (2.2.6).
