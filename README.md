# Wiki

A simple Git-backed wiki, with a clean reading view and a dual-pane Markdown/WYSIWYG editor.

## Run

Open `index.html` locally or enable GitHub Pages for this repository (Settings → Pages → Deploy from branch → `master` → `/ (root)`).

Enter a repository name such as `owner/wiki-content`, or navigate directly to:

`https://mbligh.github.io/wiki/#/owner/wiki-content/index.md`

The target repository should contain Markdown files. Directories can have an `index.md` landing page. Content is loaded on demand from GitHub; no publishing or site rebuild is needed after editing.

## Editing

Click **GitHub token** and supply a fine-grained personal access token with Contents read/write access to the relevant data repository. The token is stored in sessionStorage for the current browser session. Click **Edit**, modify either Markdown or WYSIWYG pane, and **Save** to commit directly to GitHub. To clear the token, click the token button and submit an empty value.

This is an MVP; do not share a token or use a broadly scoped token. GitHub Pages hosts the frontend publicly; private content is fetched through authenticated GitHub API requests.

See [project.md](project.md) for architecture, decisions and limitations.
