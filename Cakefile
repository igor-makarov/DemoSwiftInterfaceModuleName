require 'yaml'

project.name = 'DemoSwiftInterfaceModuleName'

target do |t|
  t.name = 'Library1'
  t.type = :framework
  t.platform = :ios
  t.deployment_target = '14.0'
  t.all_configurations.each do |configuration|
    configuration.settings['BUILD_LIBRARY_FOR_DISTRIBUTION'] = 'YES'
    configuration.settings['SWIFT_INSTALL_OBJC_HEADER'] = 'NO'
  end
end if ENV['CREATE_FRAMEWORK']

application_for :ios, '14.0' do |target|
  target.name = 'App'
  target.include_files = [
    'App/**/*',
    'build/Debug-iphonesimulator/Library1.framework'
  ]
  target.all_configurations.each do |config|
    config.product_bundle_identifier = 'com.igor.demoswiftinterfacemodulename'
    config.settings['FRAMEWORK_SEARCH_PATHS'] = '$(inherited) ${SRCROOT}/build/Debug-iphonesimulator'
    config.settings['SWIFT_INCLUDE_PATHS'] = '$(inherited) ${SRCROOT}/build/Debug-iphonesimulator'
  end
end

project.after_save do
  system "rm -rf \"#{project.name}.xcodeproj/xcshareddata/xcschemes\""
end
