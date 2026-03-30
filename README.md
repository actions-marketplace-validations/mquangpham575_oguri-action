# 🏃‍♂️ Oguri Run GitHub Action

Automatically generate an animated SVG of the **Oguri Gourmet** (from Umamusume) "eating" your GitHub contributions!

![Oguri Run Example](https://raw.githubusercontent.com/mquangpham575/mquangpham575/main/public/oguri-run.svg)

## 🚀 Usage

Add the following step to your GitHub Actions workflow:

```yaml
- name: Generate Oguri Run
  uses: YOUR_USERNAME/oguri-action@main
  with:
    # GitHub username to fetch contributions for (default: repo owner)
    github_user_name: 'mquangpham575'
    
    # Where to save the generated SVG (relative to workspace)
    svg_out_path: 'dist/oguri-run.svg'
  env:
    # Required to fetch private/public contribution data
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

      - name: Generate SVG
        uses: YOUR_USERNAME/oguri-action@main
        with:
          github_user_name: 'mquangpham575'
          svg_out_path: 'oguri-run.svg'
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Commit & Push
        uses: EndBug/add-and-commit@v9
        with:
          message: 'Update Oguri Run SVG'
          add: 'oguri-run.svg'
```

## 🎨 Options

| Input | Description | Default |
| :--- | :--- | :--- |
| `github_user_name` | The GitHub user whose contribution graph will be shown. | Repository Owner |
| `svg_out_path` | The path where the SVG file will be created. | `oguri-run.svg` |
| `github_token` | The token used to call the GitHub API. | `${{ github.token }}` |

## 🌟 License
MIT
