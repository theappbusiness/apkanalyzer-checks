# Analyze APK in GitHub Actions workflows

This GitHub Action can be used to analyze an APK file in github actions workflows to capture the following information
 - File size (in human readable format e.g. 15Mb)
 - APK download size (in human readable format e.g. 15Mb)
 - APK download size in bytes (e.g. 15343)

## Inputs
- `file-path` - The path to the apk file
- `generate-summary` - `false` to disable Job summary from being generated for this check

## Outputs
- `apk-file-size` - The APK file size in human readable format
- `apk-download-size` - The APK download size in human readable format
- `apk-download-size-bytes` - The APK download size in bytes

## Use the action
```yaml
name: Check APK
on: push
jobs:
  apk-check:
    steps:
    - name: Analyse APK
      id: analyze-apk
      uses: shavinda/apkanalyzer-checks@main
      with:
        file-path: app/build/outputs/apk/debug/app-debug.apk
        generate-summary: false

    - name: Capture Info from APK Analyze
        run: |
          {
            echo "### Outputs from apkanalyzer-checks action"
            echo ""
            echo "File Size = ${{ steps.analyze-apk.outputs.apk-file-size }}"
            echo "Download Size = ${{ steps.analyze-apk.outputs.apk-download-size }}"
            echo "Download Size Bytes = ${{ steps.analyze-apk.outputs.apk-download-size-bytes }}"
          } >> $GITHUB_STEP_SUMMARY
```
