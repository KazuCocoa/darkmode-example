This project is an example to force darkmode enable by overrideUserInterfaceStyle
if the process has 'test_darkmode' process arguments.


# Handles `UserInterfaceStyle` by process arguments

In `SceneDelegate.swift`

```swift
if ProcessInfo.processInfo.arguments.contains("test_dardmode") {
    window.overrideUserInterfaceStyle = .dark
}
```

# Build

```
xcodebuild -sdk iphonesimulator -scheme darkmode-example -derivedDataPath ./build
```

# Run

```ruby
caps = {
  desired_capability: {
    platformName: :ios,
    automationName: :xcuitest,
    app: 'path/to/build/Build/Products/Debug-iphonesimulator/darkmode-example.app',
    deviceName: 'iPhone Xs Max',
    platformVersion: '13.1',
    processArguments: { args: ['test_dardmode'] }
  }
}
@driver = ::Appium::Core.for(caps).start_driver
```

## With 'processArguments: { args: ['test_dardmode'] }'

```
> @driver.execute_script('mobile: activeAppInfo', {})
#=> {"processArguments"=>{"env"=>{}, "args"=>["test_dardmode"]}, "name"=>"", "pid"=>27048, "bundleId"=>"com.kazucocoa.darkmode-example"}
```

## Without 'processArguments: { args: ['test_dardmode'] }'

```
> @driver.execute_script('mobile: activeAppInfo', {})
#=> {"processArguments"=>{"env"=>{}, "args"=>[]}, "name"=>"", "pid"=>28154, "bundleId"=>"com.kazucocoa.darkmode-example"}
```

# License
