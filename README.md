# 🏃‍♂️ Oguri Run GitHub Action

Automatically generate an animated SVG of the **Oguri Gourmet** (from Umamusume) "eating" your GitHub contributions!

<p align="center">
  <img src="https://raw.githubusercontent.com/mquangpham575/mquangpham575/gh-pages/oguri-run.svg" alt="Oguri Run" />
</p>

## 🚀 Usage

Add the following step to your GitHub Actions workflow:

```yaml
- name: generate oguri-run.svg
  uses: mquangpham575/oguri-action@v1
  with:
    github_user_name: ${{ github.repository_owner }}
    outputs: |
      dist/oguri-run.svg
      dist/oguri-run-dark.svg?palette=github-dark
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## 🛠 Full Example Workflow

```yaml
name: Generate Oguri SVG
on:
  schedule:
    - cron: "0 * * * *" # Runs every hour
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: generate oguri-run.svg
        uses: mquangpham575/oguri-action@v1
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/oguri-run.svg
            dist/oguri-run-dark.svg?palette=github-dark
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: push oguri-run.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## 🌟 License

MIT
