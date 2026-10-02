# Shiva Goud — Personal Website

A small, multi-page personal website introducing Shiva Goud and linking to his background, projects, and contact details. It is built from static files, so it does not need a database, backend, build step, or JavaScript.

## Pages and features

- **Home** (`index.html`): introduction and links to the other pages.
- **About** (`about.html`): a short background and current focus.
- **Projects** (`projects.html`): links to the GitHub profile.
- **Contact** (`contact.html`): links to LinkedIn and provides an email link.
- **Styles** (`assets/styles.css`): shared colors, layout, responsive styling, and accessibility details.

The pages use semantic HTML elements, regular links between pages, and a shared stylesheet. CSS provides the visual design and mobile layout. No JavaScript or external font downloads are required. The pages use relative links, so the same files work locally and under the repository path on GitHub Pages.

## Project structure

```text
.
├── index.html
├── about.html
├── projects.html
├── contact.html
├── assets/
│   └── styles.css
└── .github/
    └── workflows/
        └── ...  GitHub Pages workflow selected in GitHub
```

## Preview on your computer

Open `index.html` in a browser, or run Python's simple local web server from this directory:

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Then open <http://127.0.0.1:8000>. Stop the server with `Ctrl+C`.

## Publish with GitHub Pages

The repository is configured to use the **GitHub Actions → Static HTML** Pages workflow. Keep the website files at the repository root, with `index.html` directly beside this README and `assets/styles.css` in the `assets` directory. Keep the workflow file under `.github/workflows/`.

When the files are pushed to the repository's default branch, GitHub Actions deploys them. To publish an update:

1. Edit the relevant HTML or CSS files.
2. Upload or push the changed files to the repository's default branch.
3. Check the **Actions** tab and wait for the Pages deployment workflow to succeed.
4. Open the site URL shown under **Settings → Pages**.

For a project repository, the URL is typically `https://<username>.github.io/<repository-name>/`.

## Personal links

- GitHub projects: <https://github.com/shivaninja>
- LinkedIn: <https://www.linkedin.com/in/shiva-goud-2a5585351/>
- Email: <mailto:shiva79goud@gmail.com>
