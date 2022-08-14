load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_jar")

http_archive(
    name = "build_bazel_rules_apple",
    sha256 = "0052d452af7742c8f3a4e0929763388a66403de363775db7e90adecb2ba4944b",
    urls = [
        "https://github.com/bazelbuild/rules_apple/releases/download/0.31.3/rules_apple.0.31.3.tar.gz",
    ],
)

# rules_nodejs
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "ee3280a7f58aa5c1caa45cb9e08cbb8f4d74300848c508374daf37314d5390d6",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/5.5.1/rules_nodejs-5.5.1.tar.gz"],
)

load("@build_bazel_rules_nodejs//:repositories.bzl", "build_bazel_rules_nodejs_dependencies")

build_bazel_rules_nodejs_dependencies()

load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories")

node_repositories(
    node_repositories = {
        "16.14.0-darwin_amd64": ("node-v16.14.0-darwin-x64.tar.gz", "node-v16.14.0-darwin-x64", "26702ab17903ad1ea4e13133bd423c1176db3384b8cf08559d385817c9ca58dc"),
        "16.14.0-darwin_arm64": ("node-v16.14.0-darwin-x64.tar.gz", "node-v16.14.0-darwin-x64", "26702ab17903ad1ea4e13133bd423c1176db3384b8cf08559d385817c9ca58dc"),
        "16.14.0-linux_amd64": ("node-v16.14.0-linux-x64.tar.xz", "node-v16.14.0-linux-x64", "0570b9354959f651b814e56a4ce98d4a067bf2385b9a0e6be075739bc65b0fae"),
    },
    node_version = "16.14.0",
)

load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")

yarn_install(
    name = "npm",
    exports_directories_only = True,
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

### rules_js
http_archive(
    name = "aspect_rules_js",
    sha256 = "538049993bec3ee1ae9b1c3cd669156bca04eb67027b222883e47b0a2aed2e67",
    strip_prefix = "rules_js-1.0.0",
    url = "https://github.com/aspect-build/rules_js/archive/refs/tags/v1.0.0.tar.gz",
)

load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_js_dependencies()

load("@rules_nodejs//nodejs:repositories.bzl", "DEFAULT_NODE_VERSION", "nodejs_register_toolchains")

nodejs_register_toolchains(
    name = "nodejs",
    node_version = DEFAULT_NODE_VERSION,
)

load("@aspect_rules_js//npm:npm_import.bzl", "npm_translate_lock")

npm_translate_lock(
    name = "npmv2",
    lifecycle_hooks_exclude = [
        "@parcel/watcher",
    ],
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

load("@npmv2//:repositories.bzl", "npm_repositories")

npm_repositories()
