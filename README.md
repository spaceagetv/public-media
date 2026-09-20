# public-media

Static assets for Space Age TV desktop applications that must be fetchable
**anonymously over HTTPS, by end users' machines, at install time**.

Files are served through GitHub's raw endpoint, for example:

```
https://github.com/spaceagetv/public-media/raw/main/icon_1024x1024.ico
```

## Why this repository exists

Some build and installer tooling requires a fully qualified public HTTP(S) URL
rather than a local file path. Windows installers built with Squirrel are the
main case: the `iconUrl` value is written into the generated NuGet `.nuspec`,
and Windows downloads it **on the end user's machine when the app is
installed** to use as the application's icon in Control Panel → Programs and
Features. Local paths and `file:` URLs are rejected outright.

That means the asset has to be reachable without authentication, from anywhere,
by anyone running an installer.

## Before you change anything

**Do not rename, move or delete a file that is already here.**

Installers bake the asset URL in **at build time** and fetch it **at install
time**. Every release that has ever shipped keeps pointing at the URL that was
current when it was built. If a file disappears or moves, the icon silently
breaks for every previously released build, including ones users install years
from now.

To update an asset:

1. Replace the file **in place**, keeping the exact same filename.
2. Keep the same format and a comparable size. The `.ico` must remain a real
   multi-resolution Windows icon, not a renamed PNG.
3. Expect a delay. GitHub's raw endpoint caches aggressively, so a change can
   take several minutes to be served everywhere.

Adding a genuinely new asset is fine. Removing one is not.

## Contents

| File | Used by |
| --- | --- |
| `icon_1024x1024.ico` | Windows installer — Programs and Features entry |
