
````markdown
# 🗓 Daily Commit - GitHub Actions

This repository contains a simple **GitHub Actions workflow** that automatically makes a commit every day.  
It can be useful for **keeping your GitHub streak alive** or testing automation.

---

## ⚙️ How It Works
The workflow runs every day at **06:00 UTC** (around **10:30 AM IRST**).  
You can also trigger it manually from the **Actions** tab.

Steps performed:
1. **Checkout** – Clones the repository into the GitHub Actions runner.
2. **Make a change** – Appends a line with the current date and message to `log.txt`.
3. **Commit changes** – Configures Git, commits the change, and pushes it back to the repository.

---

## 📄 Workflow File (`.github/workflows/daily-commit.yml`)
```yaml
name: Daily Commit

on:
  schedule:
    - cron: "0 6 * * *" # Every day at 06:00 UTC (10:30 AM IRST)
  workflow_dispatch:

jobs:
  commit:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          persist-credentials: false

      - name: Make a change
        run: |
          echo "$(date) - commit by GitHub Actions" >> log.txt

      - name: Commit changes
        run: |
          git config user.name "Matin-Talkhabi"
          git config user.email "matintalkhabidev@gmail.com"
          git add .
          git commit -m "daily commit - $(date)" || echo "nothing to commit"
          git push https://x-access-token:${{ secrets.GITHUB_TOKEN }}@github.com/${{ github.repository }} HEAD:main
````

---

## 🔑 Notes

* **`GITHUB_TOKEN`** is provided automatically by GitHub Actions; no need to create one manually.
* The workflow will only commit if there are changes in the repository.
* You can adjust the schedule by editing the `cron` expression.
* If you fork this repository, make sure to enable GitHub Actions in your repo settings.

---

## 📚 Resources

* [GitHub Actions Documentation](https://docs.github.com/en/actions)
* [Cron Syntax](https://crontab.guru/)

---

```


