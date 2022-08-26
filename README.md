# Vulkan dependencies

Exists to host the dependencies needed to build Vulkan programs.
This lets [Bazel](https://bazel.build) build and run programs without
relying on the system having the Vulkan SDK installed.

## Example usage

WORKSPACE.bazel:

```py
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

vulkan_mac_deps_version = "1.3.211.0"

http_archive(
    name = "com_github_goki_vulkan_mac_deps",
    sha256 = "8d3277edf13a29703fc8922e32cf6e15a67c2af67c89fb1bec4dc2bce3e0cbf6",
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
            "@com_github_goki_vulkan_mac_deps//:libmoltenvk_dylib",
        ],
        "//conditions:default": [],
    }),
    ...
)
```
