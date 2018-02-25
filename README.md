# EXPERIMENTAL PROTOTYPE

This repo illustrates a proposal to simplify versioning for Bazel projects using
rules_nodejs, rules_typescript, Angular, etc.

# Usage

Install Bazel.

`$ bazel run :install`

To add dependencies, do something like

`bazel run :install -- add -D typescript`
