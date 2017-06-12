fastlane documentation
================
# Installation

Make sure you have the latest version of the Xcode command line tools installed:

```
xcode-select --install
```

## Choose your installation method:

<table width="100%" >
<tr>
<th width="33%"><a href="http://brew.sh">Homebrew</a></td>
<th width="33%">Installer Script</td>
<th width="33%">Rubygems</td>
</tr>
<tr>
<td width="33%" align="center">macOS</td>
<td width="33%" align="center">macOS</td>
<td width="33%" align="center">macOS or Linux with Ruby 2.0.0 or above</td>
</tr>
<tr>
<td width="33%"><code>brew cask install fastlane</code></td>
<td width="33%"><a href="https://download.fastlane.tools/fastlane.zip">Download the zip file</a>. Then double click on the <code>install</code> script (or run it in a terminal window).</td>
<td width="33%"><code>sudo gem install fastlane -NV</code></td>
</tr>
</table>
# Available Actions
## iOS
### ios testflight_staging
```
fastlane ios testflight_staging
```
Submit a new iOS staging build to Apple TestFlight
### ios testflight_live
```
fastlane ios testflight_live
```
Submit a new iOS live build to Apple TestFlight
### ios release
```
fastlane ios release
```
Submit a new iOS build to iTunes Connect

----

## Android
### android testfairy_staging
```
fastlane android testfairy_staging
```
Submit a new Android staging build to TestFairy
### android testfairy_live
```
fastlane android testfairy_live
```
Submit a new Android live build to TestFairy
### android build_debug
```
fastlane android build_debug
```
Install a new debug build on connected Android devices
### android build_release
```
fastlane android build_release
```
Install a new release build on connected Android devices
### android clean
```
fastlane android clean
```
Gradle clean

----

This README.md is auto-generated and will be re-generated every time [fastlane](https://fastlane.tools) is run.
More information about fastlane can be found on [fastlane.tools](https://fastlane.tools).
The documentation of fastlane can be found on [docs.fastlane.tools](https://docs.fastlane.tools).
