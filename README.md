# Vulkan dependencies

Exists to host the dependencies needed to build Vulkan programs.
This lets [Bazel](https://bazel.build) build and run programs without
relying on the system having the Vulkan SDK installed.

## Example usage

WORKSPACE.bazel:

```py
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

vulkan_mac_deps_version = "TODO"

http_archive(
    name = "com_github_goki_vulkan_mac_deps",
    sha256 = "TODO",
    url = "TODO",
    strip_prfix = "TODO",
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
