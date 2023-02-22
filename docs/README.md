# Community docs

This directory contains all the documentation for the OpenXLA website, written
in Markdown. It also includes `website` files that are used by the MkDocs build,
which is defined by `mkdocs.yml` in the repo root.

## Stage the website locally

It's easy to preview the rendered docs locally:

1. Start a Python virtual environment (optional but recommended):

    ```bash
    python3 -m venv ~/.venvs/mkdocs

    source ~/.venvs/mkdocs/bin/activate
    ```

2. Navigate to the `community` root directory, and then
   install Material for MkDocs and other packages:

    ```bash
    pip install -r docs/website/requirements.txt
    ```

3. Now start the local server:

    ```bash
    mkdocs serve
    ```

4. Open a browser to http://localhost:8000/.

That's it. The web pages automatically reload while you edit the markdown.

To stage the site, run the following command, replacing `<your remote>` with
the name of your remote repository:

```bash
mkdocs gh-deploy --remote-name <your remote>
```

This force pushes to `gh-pages` on `<your remote>`.

To learn more about publishing with mkdocs, see the following resources:

* [Deploying your docs](https://www.mkdocs.org/user-guide/deploying-your-docs/)
* [Publishing your site](https://squidfunk.github.io/mkdocs-material/publishing-your-site/)
