# 📊 Guide: How to Create a Dynamic Metrics Infographic on Your GitHub Profile

This step-by-step guide explains how to set up an automated statistics card for your GitHub profile main page using the **GitHub Metrics** tool (by *lowlighter*). This workflow includes fixes for common permission issues and API rate limits.

---

## 🚀 Step-by-Step Setup Process

### Step 1. Generate a Personal Access Token (PAT)
The script needs a special key to fetch data about your commits and repositories.

1. Go to your GitHub **Settings** ➔ **Developer settings** ➔ **Personal access tokens** ➔ **Tokens (classic)**.
2. Click the **Generate new token (classic)** button.
3. Give your token a name (e.g., `Metrics`) and set the expiration to *No expiration*.
4. Check the following scopes (permissions):
   * `repo` (all sub-items)
   * `read:user`
   * `read:org`
5. Click **Generate token** at the bottom of the page.
6. **Make sure to copy the generated token code.** It will only be displayed once!

### Step 2. Add the Token to Your Repository Secrets
1. Go to your special profile repository (the one named exactly after your GitHub username).
2. Click the **Settings** tab in the top menu.
3. In the left sidebar, choose **Secrets and variables** ➔ **Actions**.
4. Click the **New repository secret** button.
5. In the **Name** field, enter exactly in uppercase: `METRICS_TOKEN`.
6. In the **Secret** field, paste the token code you copied in Step 1.
7. Click **Add secret**.

### Step 3. Enable Write Permissions for GitHub Actions
By default, automated scripts do not have permission to create or modify files in your repository. This triggers the `Resource not accessible by integration` error.

1. In your repository **Settings**, go to the left menu and select **Actions** ➔ **General**.
2. Scroll down to the very bottom to the **Workflow permissions** section.
3. Change the setting to **Read and write permissions**.
4. Click the **Save** button.

### Step 4. Create the Action Workflow Configuration File
1. Go to the **Code** tab of your repository.
2. Create a new file at the following path: `.github/workflows/metrics.yml`.
3. Paste this optimized configuration code into the editor (problematic plugins like *PageSpeed* and *Habits* are disabled to avoid API rate limits and errors):

```yaml
name: Metrics
on:
  # Automatically runs every day at midnight
  schedule: [{cron: "0 0 * * *"}]
  # Allows triggering the script manually via a button
  workflow_dispatch:
jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write # Explicit permission to write files
    steps:
      - uses: lowlighter/metrics@latest
        with:
          token: \${{ secrets.METRICS_TOKEN }}
          user: YOUR_GITHUB_USERNAME # Replace with your GitHub login
          template: classic
          base: header, activity, community, repositories, metadata
          config_timezone: Europe/London # Set your preferred timezone (e.g., Europe/Moscow)
          
          # Programming languages plugin configuration
          plugin_languages: yes
          plugin_languages_sections: most-used, percentages
          plugin_languages_details: bytes-size, percentage
          
          # Disabled unstable plugins to prevent API rate limits and authentication errors
          plugin_habits: no
          plugin_pagespeed: no
```
4. Click **Commit changes** to save the file.

### Step 5. Trigger the First Manual Generation Run
You don't need to wait until midnight to see the result. Run it manually:
1. Navigate to the **Actions** tab of your repository.
2. Select the **Metrics** workflow in the left column.
3. Click the grey **Run workflow** dropdown on the right ➔ click the green **Run workflow** button.
4. Wait 1-2 minutes until the status icon (circle) turns **green**. 
5. A file named `github-metrics.svg` will be automatically generated in your repository root.

### Step 6. Display the Infographic on Your Profile Page
1. Open your main profile **`README.md`** file in edit mode.
2. Insert a relative link pointing to the generated image:

```markdown
![GitHub Metrics](github-metrics.svg)
```
3. Save the changes by clicking **Commit changes**.

> 💡 **Tip:** If the page still displays old data or errors after saving, force-refresh your browser cache by pressing **`Ctrl + F5`** (or `Cmd + Shift + R` on Mac).

---
Based on the profile setup experience of [KostZen](https://github.com).
