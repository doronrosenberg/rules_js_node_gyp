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
        "18.9.0-darwin_amd64": ("node-v18.9.0-darwin-x64.tar.gz", "node-v18.9.0-darwin-x64", "dce1144cbfc01e03c2e84582461c3ce83541968b2b52a3d3a6f2bbfb09183fba"),
        "18.9.0-darwin_arm64": ("node-v18.9.0-darwin-x64.tar.gz", "node-v18.9.0-darwin-x64", "dce1144cbfc01e03c2e84582461c3ce83541968b2b52a3d3a6f2bbfb09183fba"),
        "18.9.0-linux_amd64": ("node-v18.9.0-linux-x64.tar.xz", "node-v18.9.0-linux-x64", "0137e43f5492dd97b6ef1f39ea4581975016e5f1e70db461d7292c6853ace066"),
    },
    node_version = "18.9.0",
    yarn_version = "1.22.19",
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
    sha256 = "0707a425093704fab05fb91c3a4b62cf22dca18ea334d8a72f156d4c18e8db90",
    strip_prefix = "rules_js-1.3.1",
    url = "https://github.com/aspect-build/rules_js/archive/refs/tags/v1.3.1.tar.gz",
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
    lifecycle_hooks_no_sandbox = False,
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
    lifecycle_hooks_exclude = [
        "gc-stats",
    ],
)

load("@npmv2//:repositories.bzl", "npm_repositories")

npm_repositories()