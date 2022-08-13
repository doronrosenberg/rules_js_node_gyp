While migrating an exiting Bazel repo that uses Parcel bundler, ran into this issue.

The old rules_nodejs build works fine and generated our bundle:
```
  bazel build //ui:oldbuild
```

Switching to rules_js dies on node-gyp on MacOS with M1:

```
> bazel build //ui:build
DEBUG: /private/var/tmp/_bazel_doron/ac53334175a3477d9a99bff3ce5b5ec4/external/aspect_rules_js/js/private/js_run_binary.bzl:265:14: WARNING: //ui:build is not configured to produce outputs.

If this is a generated bin from package_json.bzl, consider using the *_binary variant instead.
INFO: Analyzed target //ui:build (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
ERROR: /Users/doron/git/rules_js_node_gyp/BUILD:7:22: Running lifecycle hooks on npm package @parcel/watcher@2.0.5 failed: (Exit 1): lifecycle-hooks.sh failed: error executing command bazel-out/darwin_arm64-opt-exec-2B5CBBC6/bin/external/aspect_rules_js/npm/private/lifecycle/lifecycle-hooks.sh @parcel/watcher ../../../external/npmv2__at_parcel_watcher__2.0.5/package ... (remaining 1 argument skipped)

Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging
node:internal/modules/cjs/loader:936
  throw err;
  ^

Error: Cannot find module '/private/var/tmp/_bazel_doron/ac53334175a3477d9a99bff3ce5b5ec4/sandbox/darwin-sandbox/200/execroot/__main__/bazel-out/darwin_arm64-opt-exec-2B5CBBC6/bin/node_modules/.aspect_rules_js/@parcel+watcher@2.0.5/node_modules/@parcel/node-gyp-build/bin.js'
    at Function.Module._resolveFilename (node:internal/modules/cjs/loader:933:15)
    at Function.Module._load (node:internal/modules/cjs/loader:778:27)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:77:12)
    at node:internal/main/run_main_module:17:47 {
  code: 'MODULE_NOT_FOUND',
  requireStack: []
}
Error: @parcel/watcher@2.0.5 install: `node-gyp-build`
Exit status 1
    at EventEmitter.<anonymous> (/private/var/tmp/_bazel_doron/ac53334175a3477d9a99bff3ce5b5ec4/sandbox/darwin-sandbox/200/execroot/__main__/bazel-out/darwin_arm64-opt-exec-2B5CBBC6/bin/external/aspect_rules_js/npm/private/lifecycle/lifecycle-hooks.sh.runfiles/aspect_rules_js/npm/private/lifecycle/min/index.min.js:1:73342)
    at EventEmitter.emit (node:events:520:28)
    at ChildProcess.<anonymous> (/private/var/tmp/_bazel_doron/ac53334175a3477d9a99bff3ce5b5ec4/sandbox/darwin-sandbox/200/execroot/__main__/bazel-out/darwin_arm64-opt-exec-2B5CBBC6/bin/external/aspect_rules_js/npm/private/lifecycle/lifecycle-hooks.sh.runfiles/aspect_rules_js/npm/private/lifecycle/min/index.min.js:1:79804)
    at ChildProcess.emit (node:events:520:28)
    at maybeClose (node:internal/child_process:1092:16)
    at Process.ChildProcess._handle.onexit (node:internal/child_process:302:5) {
  errno: 1,
  code: 'ELIFECYCLE',
  pkgid: '@parcel/watcher@2.0.5',
  stage: 'install',
  script: 'node-gyp-build',
  pkgname: '@parcel/watcher'
}

> @parcel/watcher@2.0.5 install /private/var/tmp/_bazel_doron/ac53334175a3477d9a99bff3ce5b5ec4/sandbox/darwin-sandbox/200/execroot/__main__/bazel-out/darwin_arm64-opt-exec-2B5CBBC6/bin/node_modules/.aspect_rules_js/@parcel+watcher@2.0.5/node_modules/@parcel/watcher
> node-gyp-build

Target //ui:build failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 0.981s, Critical Path: 0.75s
INFO: 198 processes: 142 internal, 18 darwin-sandbox, 38 local.
FAILED: Build did NOT complete successfully
```