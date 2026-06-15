# GitHub Pages deployment

## Upload the package

1. Create a new GitHub repository.
2. Upload every file from this folder to the repository root.
3. Commit the files to the default branch, normally `main`.
4. Open **Settings → Pages**.
5. Under **Build and deployment**, select **Deploy from a branch**.
6. Select the `main` branch and the `/ (root)` folder, then save.

GitHub Pages will publish `index.html` as the site entry point.

## Test mode

After publication, append the following query string to the site URL:

```text
?test=1
```

This opens the completed sample passport and exposes the sample report and JSON downloads.

To trigger the sample PDF download automatically:

```text
?test=1&download=pdf
```

## Local test

From the repository folder, run:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/
```
