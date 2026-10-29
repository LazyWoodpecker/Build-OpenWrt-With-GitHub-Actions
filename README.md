# Build OpenWrt With GitHub Actions

![GitHub](https://img.shields.io/badge/license-MIT-blue.svg) ![GitHub last commit](https://img.shields.io/github/last-commit/LazyWoodpecker/Build-OpenWrt-With-GitHub-Actions)

This repository automates building custom OpenWrt firmware using GitHub Actions, inspired by [P3TERX/Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt). It supports scheduled builds, firmware uploads to GitHub Releases. The setup is highly customizable and user-friendly.

---

## ✨ Features

-  **Scheduled Builds**: Run builds automatically or manually.
-  **Firmware Upload**: Publishes firmware files to GitHub Releases and Artifacts.
-  **Cache**: Use cache to reduce time between builds.
-  **Customizable**: Adjust source, branch, config, and DIY scripts easily.

---

## ✅ Prerequisites

📋 Ensure you have:

-  A GitHub Personal Access Token with "Contents" and "Workflows" write permission. [Guide](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).
-  An OpenWrt `.config` file (generate via `make menuconfig` or copy from another source).

---

## 🛠️ Setup Instructions

📝 Follow these steps:

1. **Fork this Repository**

2. **Set GitHub Secrets**:
   -  Go to **Settings > Secrets and variables > Actions > Secrets**.
   -  Add:
     - `RELEASES_TOKEN`: GitHub Personal Access Token.

3. **Customize Workflow**:
   - Edit `.github/workflows/build-openwrt.yml`:
     - `REPO_URL`: OpenWrt source (default: `https://github.com/openwrt/openwrt`).
     - `REPO_BRANCH`: Branch (default: `master`).
     - `CONFIG_FILE`: Config file path (default: `.config`).
     - `DIY_P1_SH`/`DIY_P2_SH`: Custom script paths.
     - `TZ`: Timezone (default: `UTC`).
     - `schedule.cron`: Build schedule (default: weekly Sundays, midnight UTC).
   - Modify `diy-part1.sh` (e.g., add feeds) and `diy-part2.sh` (e.g., change IP).

4. **Add Configuration**:
   -  Place `.config` in the repository root. Generate via `make menuconfig` locally.
   -  Ensure `.config` matches `REPO_URL` to avoid build failures.

5. **Trigger Build**:
   -  Manually trigger via **Actions > Build OpenWrt > Run workflow**.
   -  Scheduled builds run per `cron` schedule.

---

## ⚠️ Troubleshooting

- **Build Fails**: Check Actions logs. Verify `.config` compatibility with `REPO_URL`. Run `make V=s` locally to debug.
- **No Release**: Ensure `RELEASES_TOKEN` has `public_repo` scope.
- **Storage Full**: Cleanup retains 30 days of runs and 5 releases. Reduce `retain_days` or `keep_latest` if needed.

---

## ⚠️ Notes

- **SSH access**: The original version allowed SSH access to job using tmate public servers, but those servers were taken down in 2025, so I commented out the code.  --LazyWoodpecker

---

## 🙌 Credits

- Shamelessly stolen from **hhai93/Build-OpenWrt-With-GitHub-Actions**.
- **P3TERX/Actions-OpenWrt** for the original template and guide.
