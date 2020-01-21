workspace(name = "repro", managed_directories = {"@npm": ["node_modules"]})

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "c97bf38546c220fa250ff2cc052c1a9eac977c662c1fc23eda797b0ce8e70a43",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/1.1.0/rules_nodejs-1.1.0.tar.gz"],
)

http_archive(
    name = "vendored_node_10_12_0",
    build_file_content = """exports_files(["node-v10.12.0-linux-x64/bin/node"])""",
    sha256 = "4eba2e9a6db95745b769915d58e57df6ca6724ec1f023f76556fce30ceca2367",
    urls = ["https://nodejs.org/dist/v10.12.0/node-v10.12.0-linux-x64.tar.xz"],
)

load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories")

node_repositories(
    package_json = ["//:package.json"],
    vendored_node = "@vendored_node_10_12_0//:node-v10.12.0-linux-x64",
)

load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")

yarn_install(
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

load("@npm//:install_bazel_dependencies.bzl", "install_bazel_dependencies")

install_bazel_dependencies()

load("@npm_bazel_typescript//:index.bzl", "ts_setup_workspace")

ts_setup_workspace()
