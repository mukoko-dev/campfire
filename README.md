# Campfire

> **This is a fork of [basecamp/once-campfire](https://github.com/basecamp/once-campfire),
> not a Nyuchi original.** Campfire is 37signals' ONCE product, released by
> Basecamp as a Rails application under the MIT licence. Everything below this
> notice is Basecamp's own README, kept because it accurately describes the
> code.

**Upstream:** [basecamp/once-campfire](https://github.com/basecamp/once-campfire) | **Divergence:** none in application code | **Licence:** MIT (37signals)

## About this fork

The fork carries **no Nyuchi-authored application changes**. Diffing this
branch against the upstream commit it was taken from shows twelve changed
files, all of them repository plumbing: the org's shared lint gate
(`.github/workflows/lint.yml`, `.editorconfig`, `.prettierrc`,
`.prettierignore`, `.markdownlint.jsonc`, `.yamllint.yaml`), version bumps in
the existing CI and image-publishing workflows, a RuboCop tweak, and edits to
`CONTRIBUTING.md` and an issue template. No file under `app/`, `lib/`,
`config/` or `db/` differs from upstream.

The most recent upstream application commit carried here is from **2026-01-15**.
Upstream continues to develop; this fork is not currently tracking it.

If you want Campfire, take it from
[basecamp/once-campfire](https://github.com/basecamp/once-campfire). If you want
to know what Nyuchi changed, the answer is: the lint configuration, and nothing
else.

---

Campfire is a web-based chat application. It supports many of the features you'd
expect, including:

- Multiple rooms, with access controls
- Direct messages
- File attachments with previews
- Search
- Notifications (via Web Push)
- @mentions
- API, with support for bot integrations

## Deploying with Docker

Campfire's Docker image contains everything needed for a fully-functional,
single-machine deployment. This includes the web app, background jobs, caching,
file serving, and SSL.

To persist storage of the database and file attachments, map a volume to `/rails/storage`.

To configure additional features, you can set the following environment variables:

- `SSL_DOMAIN` - enable automatic SSL via Let's Encrypt for the given domain name
- `DISABLE_SSL` - alternatively, set `DISABLE_SSL` to serve over plain HTTP
- `VAPID_PUBLIC_KEY`/`VAPID_PRIVATE_KEY` - set these to a valid keypair to
  allow sending Web Push notifications. You can generate a new keypair by running
  `/script/admin/create-vapid-key`
- `SENTRY_DSN` - to enable error reporting to sentry in production, supply your
  DSN here

For example:

    docker build -t campfire .

    docker run \
      --publish 80:80 --publish 443:443 \
      --restart unless-stopped \
      --volume campfire:/rails/storage \
      --env SECRET_KEY_BASE=$YOUR_SECRET_KEY_BASE \
      --env VAPID_PUBLIC_KEY=$YOUR_PUBLIC_KEY \
      --env VAPID_PRIVATE_KEY=$YOUR_PRIVATE_KEY \
      --env TLS_DOMAIN=chat.example.com \
      campfire

## Running in development

    bin/setup
    bin/rails server

## Worth Noting

When you start Campfire for the first time, you’ll be guided through
creating an admin account.
The email address of this admin account will be shown on the login page
so that people who forget their password know who to contact for help.
(You can change this email later in the settings)

Campfire is single-tenant: any rooms designated "public" will be accessible by
all users in the system. To support entirely distinct groups of customers, you
would deploy multiple instances of the application.

## Licence

Campfire is licensed under the MIT licence by 37signals; see
[MIT-LICENSE](MIT-LICENSE). This fork adds no code and claims no copyright over
the application.
