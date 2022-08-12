# this can be seen by everything in Bazel
package(default_visibility = ["//visibility:public"])

# rules_js
load("@npmv2//:defs.bzl", "npm_link_all_packages")

npm_link_all_packages(name = "node_modules")

exports_files([
    "package.json",
])

config_setting(
    name = "fastbuild",
    values = {"compilation_mode": "fastbuild"},
)
