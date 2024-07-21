# ios
This contains the `.framework` for MoltenVK for use on iOS. To update it, [download the latest artifact from the MoltenVK repository by clicking here](https://github.com/KhronosGroup/MoltenVK/releases/latest/download/MoltenVK-ios.tar), then do:

```sh
tar -xf <path_to_file>/MoltenVK-ios.tar
```

This will make a MoltenVK directory in current dir.  Also, rename any existing good `MoltenVK.framework` to save it.  Then do:

```sh
./make-ios-framework.cosh
```

This has been verified with the 1.3.283 SDK release: https://github.com/KhronosGroup/MoltenVK/releases/tag/v1.2.9

However, the current sdk 290 (v1.2.10-rc2) file does not seem to work.

The script looks like this:

```sh
// note: not currently working
// curl -O "https://github.com/KhronosGroup/MoltenVK/releases/latest/download/MoltenVK-ios.tar"

// above unpacks into MoltenVK, move to "sdk" to avoid name conflict

[/bin/mv MoltenVK.framework MoltenVK.framework.prev]

[/bin/mv MoltenVK sdk]

[/bin/cp sdk/MoltenVK/dynamic/MoltenVK.xcframework/ios-arm64/MoltenVK.framework/MoltenVK libMoltenVK.dylib]

install_name_tool -id "@executable_path/MoltenVK.framework/MoltenVK" libMoltenVK.dylib

lipo -create libMoltenVK.dylib -output MoltenVK

mkdir MoltenVK.framework

mv MoltenVK MoltenVK.framework

cp Info.plist MoltenVK.framework/
// cosh.WriteFile("MoltenVK.framework/Info.plist", plist)

codesign --force --deep --verbose=2 --sign "60B8D28345FFB395C0C8C4DB0629CABDB93D7DBC" MoltenVK.framework

codesign -vvvv MoltenVK.framework

```

