# Figma Image Source Exporter

Bulk-copy the original links of images that stock-photo plugins (Unsplash, Pexels and others) placed in a Figma file. You no longer have to click **Tools → View image on …** one layer at a time.

It's a single static HTML page with no server or build step. It runs in your browser and talks only to Figma's API.

## How it works

Some stock-photo plugins save the photo's link on each layer they fill. You can tell because a button like **"View image on Unsplash"** appears under **Tools** in Figma's right sidebar. Figma's REST API can return that saved data through the [`plugin_data`](https://www.figma.com/developers/api#get-files-endpoint) parameter. This page asks for it and lists every link it finds.

Some images can't be recovered: ones added by plugins that don't save their source, and ones pasted or dragged in by hand. Figma doesn't keep where those came from.

## Usage

1. Open the page (locally or from your deployed URL).
2. Paste a Figma file link. To scan one frame only, right-click it, choose **Copy link to selection** and paste that. This is much faster on big files.
3. Paste a Figma personal access token: **Settings → Security → Personal access tokens**, with the *File content: read* scope.
4. List the plugins to read, one per line, as a Community page link or numeric ID. You can add a name after it:
   ```
   738454987945972471 Unsplash
   https://www.figma.com/community/plugin/<id>/<plugin-name>
   ```
   A plugin's ID is the number in its Community page link.
5. Click **Get links**, then **Copy all links** or **Download CSV**.

The **Saved data** column shows the raw data each plugin stored, which helps when a plugin saves its link in an unusual format.

## Privacy

- Your token is sent only to `api.figma.com`.
- It's kept in your browser's local storage only if you tick **Remember**.
- Nothing else is stored or sent anywhere.

## Deploy with GitHub Pages

1. Push this folder to a GitHub repository.
2. Open the repository's **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, then select `main` and `/ (root)`.
4. After a minute the page is live at `https://<your-username>.github.io/<repo-name>/`.

## Known limitations

- Each plugin saves its data its own way. The official Unsplash plugin (`738454987945972471`) is tested. For other plugins, check the **Saved data** column if links aren't recognised.
- Very large files can be slow or hit Figma's rate limits. Scan one frame at a time instead.
- Only works for files your token can access.

## Disclaimer

Not affiliated with Figma, Unsplash or any plugin author.
