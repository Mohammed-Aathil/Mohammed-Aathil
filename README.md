# ==============================
# 📄 README.md
# ==============================
# Hi 👋 I'm Mohammed Aathil J

I’m passionate about coding and open-source.  
Here’s my GitHub streak and activity 👇

---

## 🔥 Streak Stats
![GitHub Streak](https://github-readme-streak-stats.herokuapp.com/?user=USERNAME&theme=dark)

---

## 📈 Contribution Graph
![Activity Graph](https://github-readme-activity-graph.herokuapp.com/graph?username=USERNAME&theme=react-dark&area=true)


# ==============================
# ⚙️ .github/workflows/daily-streak.yml
# ==============================
name: Daily Streak

on:
  schedule:
    - cron: '0 0 * * *'   # runs daily at 00:00 UTC
  workflow_dispatch: {}   # allow manual trigger

jobs:
  streak:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
        with:
          persist-credentials: false

      - name: Update streak file
        run: |
          mkdir -p .github/streak
          echo "Last update: $(date -u '+%Y-%m-%d %H:%M:%S UTC')" >> .github/streak/streak.txt
          git add .github/streak/streak.txt

      - name: Commit & push as you
        env:
          TOKEN: ${{ secrets.PERSONAL_TOKEN }}
        run: |
          git config user.name "YOUR NAME"
          git config user.email "YOUR-EMAIL@example.com"

          git remote set-url origin https://x-access-token:${TOKEN}@github.com/${{ github.repository }}

          git commit -m "chore: daily streak update" || echo "No changes to commit"
          git push origin HEAD:${{ github.ref_name }}
