# Wiki project

## Goal
A portable Git-backed wiki with a website-like read mode and optional editing. Multiple independent content repositories share one hosted frontend. Markdown files, folders and assets remain standard Git content, with no proprietary document format or database.

## MVP architecture
- Static HTML/CSS/JavaScript frontend, hosted using GitHub Pages from this repository.
- Hash routing: `#/owner/repository/path/to/page.md`.
- GitHub REST API reads repository tree and Markdown directly, without rebuild or publishing delay.
- Folder `index.md` serves as a landing page; sidebar follows the repository hierarchy.
- markdown-it renders read mode; DOMPurify sanitizes rendered HTML.
- TOAST UI Editor provides side-by-side editable Markdown and WYSIWYG panes, synchronized after a short pause.
- GitHub Contents API commits saved pages directly to the repository's default branch, using the previously fetched blob SHA to detect conflicting writes.
- Fine-grained personal access token (Contents read/write) stored in sessionStorage; public repositories work anonymously in read mode.
- Separate repository permissions govern access; no application database.

## Design principles
1. Read mode should resemble a normal documentation website.
2. Source Markdown is canonical; no publish action and no data lock-in.
3. One frontend serves many repositories, each with its own access control.
4. Use relative Markdown links and repository-local images.
5. Favor simple, replaceable components over a complex backend.

## Current limitations / next steps
- GitHub Pages must be enabled in repository Settings → Pages (deploy from master/root).
- Browser token entry is prototype authentication; replace with GitHub App/OAuth service later.
- Edit button currently depends on token presence, not a verified per-repository permission check; failed writes are reported by GitHub.
- No create/rename/delete UI, search, upload, drag-and-drop tree or multi-file atomic commits.
- Markdown editor synchronization may reset cursor/undo history in the opposite pane.
- Raw Markdown is loaded via GitHub API; anonymous requests are rate-limited.
- Test behavior against a dedicated content repository, including private repo access.
- Review and pin CDN dependencies and implement robust link/image rewriting.
