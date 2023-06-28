# sniproxy-user-lighttpd

## What I wanted

User-controlled websites that are easy to get up and running, including HTTPS with Let's Encrypt, simply by including sysadmin-controlled shared configuration.

## What I did

1. `sniproxy` inspects and then dispatches HTTP and HTTPS requests
2. Each site is an instance of `lighttpd`, running as the user who owns it, listening on a `localhost` port to match what's in `sniproxy.conf` for that site
3. Each `lighttpd.conf` defines a few variables, includes a shared config file or two, and appends any other site-specific configuration (often none)

## What doesn't work yet

Using the shared config files, listening for HTTPS necessarily also means forcing HTTP to HTTPS. A site might want to opt out of that, instead listening on both and responding on either.

Using the shared config files, HTTP requests are always redirected to HTTPS at the value of `sitecanonical` (unless specially handled in `hosted-ssl.conf`). A site might want to define its own additional names which, if requested, are preserved.
