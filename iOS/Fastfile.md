```ruby
# This file contains the fastlane.tools configuration
# You can find the documentation at https://docs.fastlane.tools
#
# For a list of all available actions, check out
#
#     https://docs.fastlane.tools/actions
#
# For a list of all available plugins, check out
#
#     https://docs.fastlane.tools/plugins/available-plugins
#

# Uncomment the line if you want fastlane to automatically update itself
# update_fastlane

default_platform(:ios)

platform :ios do
  output_build_name = ""
  app_name = "APP名称"
  target = "target name xxxx"
  xcodeproj = "xcodeproj name xxxx"
  workspace = "xxxxx.xcworkspace"

  desc "生成名称（导出 ipa 的名称）"
  lane :generate_build_name do |options|
    # increment_version_number
    # increment_build_number
    # https://github.com/beplus/fastlane-plugin-versioning_ios

    version = get_version_number(target: target)
    build_number = get_build_number(xcodeproj: xcodeproj)
    puts "VERSION : #{version}"
    current_date = Time.new.strftime("%Y-%m-%d_%H:%M:%S")
    build_name = current_date + "-" + git_branch + "-version-"+ version + "-build-" + build_number
    output_build_name = app_name + "-" + build_name
    puts "#{app_name} BUILD NAME : #{output_build_name}"
  end

  desc "打 debug 包"
  lane :debug do |options|
    generate_build_name
    build_app(
      workspace: workspace,
      configuration: "Debug",
      scheme: "xxxx",
      silent: true,
      # clean: true,
      output_directory: "./",
      output_name: output_build_name + "-debug.ipa",
      export_method: "development"
    )
  end

  desc "打 Release 包"
  lane :release do
    generate_build_name
    build_app(
      workspace: workspace,
      configuration: "Release",
      scheme: "xxxx",
      silent: true,
      # clean: true,
      output_directory: "./",
      output_name: output_build_name + "-release.ipa",
      export_method: "ad-hoc"
    )
  end
end
```