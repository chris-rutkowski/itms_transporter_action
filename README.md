# ITMS Transporter

A GitHub Action that installs Apple's ITMS Transporter on Linux runners, allowing you to publish apps and wait for App Store processing on cheaper Linux agents instead of expensive macOS runners. While apps still need to be built on macOS, the upload and processing steps can run on Linux.

---

## 🚀 Usage

```yaml
name: Beta
on:
  workflow_dispatch:

jobs:
  ios-deploy:
    runs-on: ubuntu-latest
    needs: [ios-build] # macOS build job that creates .ipa and AppStoreInfo.plist artifacts

    steps:
      # ... checkout, download .ipa and AppStoreInfo.plist artifacts

      - name: Install ITMS Transporter
        uses: chris-rutkowski/itms_transporter_action@main

      - name: Fastlane deploy
        run: bundle exec fastlane deploy
        env:
          IPA_PATH: .../MyApp.ipa
          FASTLANE_ITUNES_TRANSPORTER_USE_SHELL_SCRIPT: true
          FASTLANE_ITUNES_TRANSPORTER_PATH: "/usr/local/itms"
          DELIVER_ITMSTRANSPORTER_ADDITIONAL_UPLOAD_PARAMETERS: "-assetDescription .../AppStoreInfo.plist"
```

---

## 📝 Notes

- ITMS Transporter will be installed to `/usr/local/itms/bin/iTMSTransporter`
- No inputs or outputs - just run it before you need to use iTMSTransporter
- ITMS Transporter is Apple's proprietary software. This action only automates its installation from Apple's official distribution endpoint

---

## 📄 License
This project is licensed under the [MIT License](LICENSE).
