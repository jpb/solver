load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

git_repository(
    name = "ortools",
    commit = "80d88b893cd35d85a9bbbce14dc26295e405ef60",  # release v9.9
    remote = "https://github.com/jpb/or-tools.git",
)

git_repository(
    name = "com_google_absl",
    commit = "2f9e432cce407ce0ae50676696666f33a77d42ac", # release 20240116.1
    remote = "https://github.com/abseil/abseil-cpp.git",
)

git_repository(
    name = "com_google_protobuf",
    commit = "4a2aef570deb2bfb8927426558701e8bfc26f2a4", # release v25.3
    remote = "https://github.com/protocolbuffers/protobuf.git",
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

# Load dependencies needed to compile protobuf.
protobuf_deps()

# TODO(irfansharif): Capture swig and protoc{-gen-go} within bazel instead of
# asking contributors to download it themselves.

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "8e968b5fcea1d2d64071872b12737bbb5514524ee5f0a4f54f5920266c261acb",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.28.0/rules_go-v0.28.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.28.0/rules_go-v0.28.0.zip",
    ],
)

git_repository(
    name = "bazel_gazelle",
    commit = "d038863ba2e096792c6bb6afca31f6514f1aeecd",
    remote = "https://github.com/bazelbuild/bazel-gazelle",
)

# Load up our go dependencies (the ones listed under go.mod). The `DEPS.bzl`
# file is kept up to date using the `update-repos` Gazelle command (see
# README).
#
# gazelle:repository_macro DEPS.bzl%go_deps
load("//:DEPS.bzl", "go_deps")

# VERY IMPORTANT that we call into this function to prefer the pinned versions
# of our dependencies instead of any that may get pulled in through like
# `go_rules_dependencies`, `gazelle_dependencies`, etc.
go_deps()

load("@io_bazel_rules_go//go:deps.bzl", "go_rules_dependencies", "go_register_toolchains")

go_rules_dependencies()

go_register_toolchains(go_version = "1.16.5")

# Load gazelle dependencies.
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()
