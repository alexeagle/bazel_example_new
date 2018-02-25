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
    url = "https://github.com/alexeagle/rules_nodejs/archive/bootstrap_published.tar.gz",
    strip_prefix = "rules_nodejs-bootstrap_published",
    sha256 = "2c10ab0842cc15c4e860ae733a25e2f67adb30257bc748f0317753033a38d8f1",
)
load("@build_bazel_rules_nodejs_bootstrap//:defs.bzl", "node_repositories")
node_repositories(package_json = ["//:package.json"])

### THAT'S THE END
### Unless the user is using other ecosystems (eg. scala rules) they shouldn't
# touch this file again or care what ends up in here.

