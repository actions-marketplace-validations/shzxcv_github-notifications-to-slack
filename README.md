# Github Notifications To Slack
<a href="https://www.repostatus.org/#active"><img src="https://www.repostatus.org/badges/latest/active.svg" alt="Project Status: Active – The project has reached a stable, usable state and is being actively developed." /></a>

Notify Slack of your github notifications, which can be scheduled to run using Github Actions.

**Slack**

<img width="508" alt="image" src="https://user-images.githubusercontent.com/68991732/190888938-52399977-b045-49e8-8afb-a028b1a5ba94.png">

You can register a white list and black list of repositories to be notified.

## Usage

1. Need to create a slack bot. Access **[Slack Applications](https://api.slack.com/apps)**.
2. **[Create new app]** -> **[From scratch]**
3. **[OAuth & Permissions]** -> Add **chat:write** to Bot Token Scopes and re install.
4. Create a github token. Access **[Personal access tokens](https://github.com/settings/tokens)**, Tokens require the score of **repo**, **notifications**.
5. Create a repository to run scheduled notifications and create the following Actions.

**.github/workflows/slack-notify.yml**
```
on:
  schedule:
    - cron: "*/10 * * * *"

jobs:
  notify:
    runs-on: ubuntu-latest
    name: notify
    steps:
      - uses: actions/checkout@v3
      - name: Github Notifications To Slack
        uses: actions/github-notifications-to-slack@v0.1
        env:
          NOTIFICATION_GITHUB_TOKEN: ${{ secrets.NOTIFICATION_GITHUB_TOKEN }}
          SLACK_BOT_OAUTH_TOKEN: ${{ secrets.SLACK_BOT_OAUTH_TOKEN }}
          SLACK_USER_ID: ${{ secrets.SLACK_USER_ID }}
```

6. Register environment variables in the Secrets repository.
