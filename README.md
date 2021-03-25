# Routify Sveltefire Starter

- Routify (created with `npx @roxi/routify init`)
- Changed `npm` to `yarn` since yarn's better
- Installed [`sveltefire`](https://github.com/codediodeio/sveltefire) and `firebase`. Sveltefire is easy middleware for Firebase.
- Put the default [Sveltefire](https://github.com/codediodeio/sveltefire-template/blob/master/src/App.svelte) page in the `index.svelte`
- Activated the Service Worker for Routify like [this](https://routify.dev/guide/starter-Template/PWA_&_offline_first)

I'm pretty sure this is the easiest way to make a web app with Firebase because:

1. Svelte is the easiest JS framework that is actually quite performant
2. Sveltefire is the easiest Firebase middleware I've ever used
3. Routify is basically the only good router for Svelte since it uses static routing, can do SSR and prerendering, etc. The other routers for Svelte require a server (like Sapper) or use hash routing (bleh).

So yea here you go. Go code and enjoy :)

## Limitations 

Cannot build SSR with Firebase Performance or Firebase Analytics because both require IndexedDB. I think there's a workaround but I haven't figured it out yet.
If someone's willing to help out I would appreciate it.

The following is the README from the default routify starter!

# routify-starter

Starter template for [Routify](https://github.com/sveltech/routify).

### Get started

#### Starter templates
| Template                                  | Description                                                 |
|-------------------------------------------|-------------------------------------------------------------|
| [master](https://example.routify.dev/)    | Default template, includes examples folder                  |
| [blog](https://blog-example.routify.dev/) | Generates a blog from local markdown posts. Includes mdsvex |
| [auth](https://auth-example.routify.dev/) | Embedded login on protected pages. Includes Auth0           |

To use a template, run:

`npx @sveltech/routify init`

or

`npx @sveltech/routify init --branch <branch-name>`

The above commands will populate the current directory, they don't create a new one.

### npm scripts

| Syntax           | Description                                                                       |
|------------------|-----------------------------------------------------------------------------------|
| `dev`            | Development (port 5000)                                                           |
| `dev:nollup`     | Development with crazy fast rebuilds (port 5000)                                  |
| `dev-dynamic`    | Development with dynamic imports                                                  |
| `build`          | Build a bundled app with SSR + prerendering and dynamic imports                   |
| `serve`          | Run after a build to preview. Serves SPA on 5000 and SSR on 5005                  |
| `deploy:*`       | Deploy to netlify or now                                                          |
| `export`         | Create static pages from content in dist folder (used by `npm run build`)         |

### SSR and pre-rendering

SSR and pre-rendering are included in the default build process.

`npm run deploy:(now|netlify)` will deploy the app with SSR and prerendering included.

To render async data, call the `$ready()` helper whenever your data is ready.

If $ready() is present, rendering will be delayed till the function has been called.

Otherwise it will be rendered instantly.

See [src/pages/example/api/[showId].svelte](https://github.com/sveltech/routify-starter/blob/master/src/pages/example/api/%5BshowId%5D.svelte) for an example.

### Production

* For SPA or SSR apps please make sure that url rewrite is enabled on the server.
* For SPA redirect to `__app.html`.
* For SSR redirect to the lambda function or express server.

### Typescript

For Typescript, we recommend [@lamualfa](https://github.com/lamualfa) excellent [routify-ts](https://github.com/lamualfa/routify-ts/)

New project: `npx routify-ts init <project-name> [routify-init-args]`

Existing project: `npx routify-ts convert [project-directory]`


### Issues?

File on Github! See https://github.com/sveltech/routify/issues .
# routify-sveltefire
