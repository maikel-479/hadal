# Publishing a Zed Theme Extension

A step-by-step guide to turning a Zed theme JSON into a publishable extension using `gh` CLI.

## Prerequisites

- [Zed](https://zed.dev) installed
- [GitHub CLI (`gh`)](https://cli.github.com/) authenticated (`gh auth login`)
- A working theme JSON file following the [Zed Theme Schema](https://zed.dev/schema/themes/v0.2.0.json)

## 1. Project Structure

```
my-theme/
  extension.toml
  README.md
  LICENSE
  assets/
    screenshot-dark.png
    screenshot-light.png
  themes/
    my-theme.json
```

## 2. Create `extension.toml`

```toml
[package]
name = "my-theme"
version = "0.1.0"
schema_version = 1
authors = ["your-github-username"]
description = "Short description of your theme"
repository = "https://github.com/your-github-username/my-theme"

[grammars]
```

- `name`: Must match your GitHub repo name
- `authors`: Your GitHub username
- `repository`: Full URL to your theme repo
- `[grammars]`: Empty — not needed for pure themes

## 3. Theme File

Place your theme JSON in `themes/my-theme.json`. The file must follow the [Zed Theme JSON Schema](https://zed.dev/schema/themes/v0.2.0.json).

Top-level structure:

```json
{
  "name": "My Theme",
  "author": "your-github-username",
  "themes": [
    {
      "name": "My Theme Dark",
      "appearance": "dark",
      "style": { ... }
    },
    {
      "name": "My Theme Light",
      "appearance": "light",
      "style": { ... }
    }
  ]
}
```

## 4. Initialize Git and Push

```bash
cd my-theme/
git init
git add -A
git commit -m "Initial release: my-theme for Zed"

# Create the GitHub repo and push
gh repo create your-github-username/my-theme --public --source=. --push
```

If SSH fails, switch to HTTPS:

```bash
git remote set-url origin https://github.com/your-github-username/my-theme.git
git push -u origin main
```

If you get an email privacy error:

```bash
git config user.email "your-github-username@users.noreply.github.com"
git commit --amend --no-edit --reset-author
git push -u origin main
```

## 5. Fork the Extensions Repo

```bash
gh repo fork zed-industries/extensions --clone=false
```

## 6. Clone Your Fork

```bash
git clone https://github.com/your-github-username/extensions.git /tmp/zed-extensions
cd /tmp/zed-extensions
```

## 7. Add Your Theme as a Submodule

```bash
git submodule add https://github.com/your-github-username/my-theme.git extensions/my-theme
```

## 8. Register in `extensions.toml`

Find the correct alphabetical position and add your entry:

```toml
[my-theme]
submodule = "extensions/my-theme"
version = "0.1.0"
```

## 9. Fix `.gitmodules` Sort Order

`git submodule add` appends to the end. You must move it to the correct sorted position.

Find where your entry should go:

```bash
grep -n "extensions/[your-letter]" .gitmodules
```

Then manually edit `.gitmodules`:
1. Remove your entry from the bottom
2. Insert it in alphabetical order among the other entries

## 10. Commit and Push

```bash
git config user.email "your-github-username@users.noreply.github.com"
git add -A
git commit -m "Add my-theme extension"
git push origin main
```

## 11. Open the PR

```bash
gh pr create \
  --repo zed-industries/extensions \
  --title "Add my-theme extension" \
  --body "Adds the [my-theme](https://github.com/your-github-username/my-theme) theme to the Zed extension store."
```

## 12. Sign the CLA

1. Go to https://zed.dev/cla and sign
2. On your PR, comment:

```
@cla-bot check
```

## 13. Wait for Review

The Zed team will review your PR. Check for feedback:

```bash
gh pr view <pr-number> --repo zed-industries/extensions --comments
```

Once merged, your theme appears in the Zed extension store automatically.

## Updating Your Theme

After the initial publish, push version bumps to your theme repo and update the version in `extensions.toml`:

```bash
# In your theme repo
git add -A
git commit -m "Bump version to 0.2.0"
git tag 0.2.0
git push origin main --tags

# In the extensions fork
# Update version in extensions.toml, then:
git add extensions.toml
git commit -m "Update my-theme to 0.2.0"
git push origin main
```

Then open a new PR with:

```bash
gh pr create \
  --repo zed-industries/extensions \
  --title "Update my-theme to 0.2.0" \
  --body "Updates my-theme from 0.1.0 to 0.2.0."
```

## Useful Commands

| Task | Command |
|---|---|
| Check PR status | `gh pr view <number> --repo zed-industries/extensions` |
| View PR comments | `gh pr view <number> --repo zed-industries/extensions --comments` |
| Test locally | Copy `themes/my-theme.json` to `~/.config/zed/themes/` |
| Design a theme | Use [Zed Theme Builder](https://zed.dev/theme-builder) |
