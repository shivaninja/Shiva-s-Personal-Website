# Build and host my personal website

This guide describes a small personal website that introduces you and links to your projects. It uses plain HTML only, with no stylesheet, framework, database, build service, or paid hosting required. Keep the site files portable so the same site can run on your own computer or on a free static hosting platform.

## 1. What you will need

- A computer with a text editor. [Visual Studio Code](https://code.visualstudio.com/) is free and open source; a basic text editor works too.
- A modern web browser.
- [Git](https://git-scm.com/) is optional for the PC-hosted version and useful for saving changes and publishing to a platform.
- An account on the hosting service you choose for the external version.

The website itself will be made with the open HTML standard and open-source tools: a text editor, Git, and optionally Nginx. Hosting providers are services, not necessarily open-source software; the source code for your website remains yours and can be moved to another host.

## 2. Create the site

Create a folder called `my-website` and add these files:

```text
my-website/
├── index.html
└── images/
    └── profile.jpg   (optional)
```

Put this starter content in `index.html`, replacing the example details and links:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="description" content="The personal website of Your Name.">
  <title>Your Name — Personal Website</title>
</head>
<body>
  <main>
    <header>
      <!-- Optional: add <img src="images/profile.jpg" alt="Your Name"> -->
      <p>Hello, I'm</p>
      <h1>Your Name</h1>
      <p>I am a [your role or area of interest] interested in [topics].</p>
    </header>

    <section aria-labelledby="about-heading">
      <h2 id="about-heading">About me</h2>
      <p>Write a short introduction: what you do, what you are learning, and what you enjoy working on.</p>
    </section>

    <section aria-labelledby="projects-heading">
      <h2 id="projects-heading">Projects</h2>
      <ul>
        <li>
          <h3><a href="https://example.com/project-one">Project One</a></h3>
          <p>A one-sentence description of what it does and what you contributed.</p>
        </li>
        <li>
          <h3><a href="https://example.com/project-two">Project Two</a></h3>
          <p>A one-sentence description of this project.</p>
        </li>
      </ul>
    </section>

    <footer>
      <p><a href="mailto:you@example.com">Email</a> · <a href="https://github.com/your-name">GitHub</a> · <a href="https://www.linkedin.com/in/your-name/">LinkedIn</a></p>
    </footer>
  </main>
</body>
</html>
```

Open `index.html` in your browser to preview it. Edit the HTML, save, then refresh the browser. Without CSS, the browser uses its built-in default presentation. Use meaningful link text, describe images with `alt` text, and avoid putting private information on a public site. You can omit the optional image entirely.

## 3. Version A — serve the site from your own PC

### Preview on your PC

For a site with only HTML, opening `index.html` is enough for a preview. A local HTTP server gives a more realistic preview. If Python 3 is already installed, open a terminal in the `my-website` folder and run:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Visit <http://127.0.0.1:8000>. Stop the server with `Ctrl+C`.

### Make it reachable on your home network

To let another device on the same Wi-Fi view it, run the server without the loopback-only bind:

```sh
python3 -m http.server 8000
```

Find your PC's local network address (for example, `192.168.1.25`) and visit `http://192.168.1.25:8000` from the other device. Keep the server running. This is for a trusted local network; Python's simple server is intended for testing, not a hardened public web server.

### Make it reachable from the public internet (optional)

This requires your PC to remain powered on and connected. Your router and internet provider must permit inbound connections. You may need to configure a static DHCP reservation for the PC, router port forwarding, a firewall, a domain or dynamic DNS name, and HTTPS. A changing home IP, carrier-grade NAT, or provider restrictions may prevent direct access. Exposing a home computer to the internet increases security risk; keep the operating system updated, expose only a dedicated web server such as Nginx, and do not expose its admin or file-sharing services. Do not expose Python's test server as a public production host.

For an Ubuntu PC, a possible starting point is to install Nginx, copy the site into its document root, then configure the router and firewall only if you understand and intend the exposure:

```sh
sudo apt update
sudo apt install nginx
sudo cp -r ./ ./   # Run the copy separately after choosing a destination; see note below.
```

The copy command above is deliberately not a usable deployment command: choose a destination such as `/var/www/my-website` and copy the site files there with appropriate permissions. Then configure an Nginx server block with that directory as its `root`. The [Ubuntu Nginx guide](https://ubuntu.com/server/docs/how-to/web-services/configure-nginx/) explains server blocks. Avoid opening router ports until the server is configured and patched. HTTPS certificates and home-network routing add extra setup; a public static host is generally simpler for a public portfolio.

**Cost note:** serving files from the PC avoids a hosting subscription, but it is not guaranteed to be cost-free overall. Electricity, internet service, domain names, equipment, or a changing-IP solution can cost money. Local network hosting is the simplest no-extra-hosting-cost option.

## 4. Version B — publish on a free external platform

For this simple site, a static host serves your existing files without needing a server process you maintain. GitHub Pages is a straightforward option for a personal portfolio; Cloudflare Pages is another option. Their hosting software and infrastructure are not themselves fully open source, but both accept ordinary static files and allow you to retain and move your source code. A custom domain is optional and usually costs money; use the free provider subdomain to keep the setup free.

### Option 1: GitHub Pages

1. Create or sign in to a GitHub account and create a repository named `your-username.github.io` (replace `your-username` with your GitHub username).
2. Put `index.html` and any images at the repository root. Do not upload secrets or private files. A public repository makes its source visible.
3. If Git is installed, from the `my-website` directory initialize and push the files (replace the URL with your repository URL):

   ```sh
   git init
   git add index.html images
   git commit -m "Create personal website"
   git branch -M main
   git remote add origin https://github.com/your-username/your-username.github.io.git
   git push -u origin main
   ```

   If you do not have an `images` folder, use `git add index.html` instead. You can also upload files through GitHub's website.
4. In the repository, open **Settings → Pages**. Select publishing from the `main` branch and the `/(root)` folder, then save.
5. Wait for the Pages deployment to finish. Visit `https://your-username.github.io` and check the page and all links.
6. For later updates, edit the files, then run `git add index.html`, `git commit`, and `git push`; GitHub Pages redeploys from the selected branch.

See the official [GitHub Pages publishing-source guide](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) and [usage limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits). GitHub documents a 1 GB published-site limit and a soft 100 GB/month bandwidth limit; its terms and limits can change. Pages is intended for project or personal sites, not as a general commercial hosting service.

### Option 2: Cloudflare Pages

Cloudflare Pages supports plain static HTML. For automatic updates after each Git push:

1. Push your site files to a GitHub or GitLab repository (the Git commands above apply; create the repository first).
2. In Cloudflare, create a Pages project using **Git integration**, connect the repository, and select the `main` branch.
3. Because this site has no build step, leave the build command empty and set the output directory to `/` or the repository root as the dashboard instructs.
4. Deploy, then use the provided `*.pages.dev` address to check the page and its links.
5. Push changes to the connected branch to trigger a new deployment.

Cloudflare also offers manual drag-and-drop/direct upload, but choose your deployment method carefully: its documentation says a direct-upload project cannot later be switched to Git integration, and a Git-integrated project cannot later be switched to direct upload. See the official [Cloudflare Pages guide](https://developers.cloudflare.com/pages/get-started/) and [free-plan limits](https://developers.cloudflare.com/pages/platform/limits/). Current docs list limits including 500 builds/month, 20,000 files per site, and 25 MiB per file on the Free plan; verify current terms before relying on these figures.

## 5. Keep a copy and update it

- Keep your `my-website` folder on your PC as the source of truth. If using Git, push changes regularly and keep a second backup if the site matters to you.
- Check external links and how the page reads on a mobile screen after changes.
- Use only images, fonts, and other assets you have permission to publish. Plain HTML needs no font downloads or external scripts.
- Recheck your provider's current free-plan terms occasionally. Free tiers can change, and providers may suspend service if usage or policy limits are exceeded.
- You can move the site later: copy the same static files to another compatible host. No framework-specific build output is required.

## Official references

- [GitHub Pages documentation](https://docs.github.com/en/pages)
- [GitHub Pages usage limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits)
- [Cloudflare Pages documentation](https://developers.cloudflare.com/pages/)
- [Cloudflare Pages limits](https://developers.cloudflare.com/pages/platform/limits/)
- [Ubuntu: Configure Nginx](https://ubuntu.com/server/docs/how-to/web-services/configure-nginx/)
- [Ubuntu: Firewall (UFW)](https://ubuntu.com/server/docs/firewalls/)
