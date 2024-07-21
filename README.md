# Vulkan dependencies

Exists to host the dependencies needed to build Vulkan programs.

see `sdk/ios` and `sdk/macOS` for further info

# Old Bazel info:

We are not using this anymore, but it might be useful to someone:

This lets [Bazel](https://bazel.build) build and run programs without
relying on the system having the Vulkan SDK installed. Also, it is used
by `goki setup` to download the `.framework` needed for building Vulkan
apps for iOS.

## Example usage

WORKSPACE.bazel:

```py
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

vulkan_mac_deps_version = "1.3.239.0"

http_archive(
    name = "com_github_goki_vulkan_mac_deps",
    sha256 = "348bc84c0fc1f1e79fb28bcf83454faa2a84c4d4c2286225d4413830a3c0a29c",
    strip_prefix = "vulkan_mac_deps-%s" % vulkan_mac_deps_version,
    url = "https://github.com/goki/vulkan_mac_deps/archive/refs/tags/%s.tar.gz" % vulkan_mac_deps_version,
)
```

BUILD.bazel:

```py
go_library(
    ...
    cdeps = select({
        "@io_bazel_rules_go//go/platform:darwin": [
            "@com_github_goki_vulkan_mac_deps//:vulkan_mac_deps",
        ],
        "//conditions:default": [],
    }),
    ...
)
```
