name: Deploy Homework to GitLab Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Git
        run: |
          git config --global user.email "your-email@example.com"
          git config --global user.name "GitHub Actions Bot"

      - name: Push to GitLab Pages
        env:
          GITLAB_TOKEN: ${{ secrets.GITLAB_TOKEN }}
        run: |
          git remote add GitLab https://oauth2:${GITLAB_TOKEN}@gitlab.com/username/my-homework.git
          git push GitLab main --force
