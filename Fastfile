# Customise this file, documentation can be found here:
# https://github.com/fastlane/fastlane/tree/master/fastlane/docs
# All available actions: https://github.com/fastlane/fastlane/blob/master/fastlane/docs/Actions.md
# can also be listed using the `fastlane actions` command

# Change the syntax highlighting to Ruby
# All lines starting with a # are ignored when running `fastlane`

fastlane_require "json"
fastlane_version "2.16.0"

platform :ios do
  before_all do
  end

  desc "Submit a new iOS staging build to Apple TestFlight"
  lane :qa do
    ios_build
    pilot
    notification(
      title: "Build complete!",
      message: "A new iOS build has finished and been submitted to TestFlight"
    )
  end

  desc "Submit a new iOS build to iTunes Connect"
  lane :release do
    ios_build
    deliver(
      force: true
    )
    notification(
      title: "Build complete!",
      message: "A new iOS build has finished and been submitted to iTunes Connect"
    )
  end

  desc "Run a new iOS build (without submission)"
  lane :dryrun do
    ios_build
    notification(
      title: "Build complete!",
      message: "A new iOS build has finished"
    )
  end

  private_lane :ios_build do |options|
    clean_build_artifacts
    clear_derived_data
    cocoapods(
      clean: true,
      integrate: true,
      podfile: "./ios"
    )
    match(
      readonly: true,
      type: "appstore"
    )
    props = JSON.parse(File.read("../properties.ios.json"))
    increment_version_number_in_plist(
      version_number: props["version"],
      xcodeproj: "./ios/App.xcodeproj",
      target: "App"
    )
    increment_build_number(
      build_number: props["build"],
      xcodeproj: "./ios/App.xcodeproj"
    )
    gym(
      scheme: "App",
      workspace: "./ios/App.xcworkspace"
    )
  end
end

platform :android do
  desc "Submit a new Android staging build to TestFairy"
  lane :qa do
    android_build(type: "Release", testfairy: true)
  end

  desc "Submit a new Android live build to TestFairy"
  lane :release do
    android_build(type: "Release", testfairy: true)
  end

  desc "Run a new Android live build"
  lane :dryrun do
    android_build(type: "Release")
  end

  desc "Install a new debug build on connected Android devices"
  lane :installdebug do
    android_build(type: "Debug")
    adb_start
  end

  desc "Install a new release build on connected Android devices"
  lane :installrelease do
    android_build(type: "Release")
    adb_start
  end

  desc "Gradle clean"
  lane :clean do
    gradle(
      task: "clean",
      project_dir: "./android"
    )
  end

  private_lane :adb_start do
    package = /package="(.+?)"/.match(File.read("../android/app/src/main/AndroidManifest.xml"))[1]
    adb_devices.each do |device|
      model = adb(command: "shell am start -n #{package}/.MainActivity", serial: device.serial)
    end
  end

  private_lane :android_build do |options|
    task = options.key?(:testfairy) ? "testfairy" : "install"
    gradle(
      task: task,
      build_type: options[:type],
      project_dir: "./android"
    )
  end
end
