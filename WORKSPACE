# Users can import using workspace paths, for example in tsickle we can
#  import {} from 'tsickle/some/deep/import'
# and it's essential that the first path segment here matches the name on NPM, so that
# these deep-imports work for users.
# Remember that users will just have standard node module resolution, yet these imports
# will be written by TypeScript without any translation.

# However, this is a problem for scoped packages. Also, it abuses the Bazel convention
# of namespacing by urls.
# Here's a proposal to encode arbitrary npm package names in Bazel:
# this is URI-encoding of com_npmjs:@bazel/example_new with %->__
workspace(name = "com_npmjs__3A__40bazel__2Fexample_new")
# That would require that we map the workspace name whenever we use it for node resolution.
# Within this repo I should be able to `import {} from '@bazel/example_new'` without any
# special path mapping or module_name on a rule.

## Bootstrapping bit to get nodejs rules
# Users will have to paste this into their WORKSPACE file to get started,
# but after that we can manage the WORKSPACE file for them.
http_archive(
    name = "build_bazel_rules_nodejs_bootstrap",
    url = "https://github.com/bazelbuild/rules_nodejs/archive/bootstrap.tar.gz",
    strip_prefix = "rules_nodejs-bootstrap",
    sha256 = "55c01a2ef46fa00da7dcaad8768df545a861e22a8803bd19643c8ec7e3b59ff7",
)
load("@build_bazel_rules_nodejs_bootstrap//:defs.bzl", "node_repositories")
node_repositories(package_json = ["//:package.json"])

### THAT'S THE END
### Unless the user is using other ecosystems (eg. scala rules) they shouldn't
# touch this file again or care what ends up in here.

#########################
# JavaScript Bazel rules
# This is added automatically by the postinstall script of @bazel/javascript

local_repository(
    # TODO: this should be named encode(com_npmjs:@bazel/javascript)
    name = "build_bazel_rules_nodejs",
    path = "node_modules/@bazel/javascript",
)
#########################
# TypeScript Bazel rules
# This is added automatically by the postinstall script of @bazel/typescript

local_repository(
    name = "build_bazel_rules_typescript",
    path = "node_modules/@bazel/typescript",
)
load("@build_bazel_rules_typescript//:defs.bzl", "ts_setup_workspace")
ts_setup_workspace()

# Some of the TypeScript tooling is written in Go.
# Bazel doesn't support transitive WORKSPACE deps, so we must repeat them here.
http_archive(
    name = "io_bazel_rules_go",
    url = "https://github.com/bazelbuild/rules_go/releases/download/0.10.0/rules_go-0.10.0.tar.gz",
    sha256 = "53c8222c6eab05dd49c40184c361493705d4234e60c42c4cd13ab4898da4c6be",
)
load("@io_bazel_rules_go//go:def.bzl", "go_rules_dependencies", "go_register_toolchains")
go_rules_dependencies()
go_register_toolchains()
