# ios
This contains the `.framework` for MoltenVK for use on iOS. To update it, [download the latest artifact from the MoltenVK repository by clicking here](https://github.com/KhronosGroup/MoltenVK/releases/latest/download/MoltenVK-ios.tar), unpack it and get the `libMoltenVk.dylib` from `MoltenVK/dylib/ios`, copy it here, and run:

```sh
gsm make-ios-framework -dylib libMoltenVk.dylib -framework MoltenVK -developer rcoreilly@me.com -organization goki
```