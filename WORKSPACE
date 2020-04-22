load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "io_bazel_rules_dotnet",
    sha256 = "6a1fa7a1b58e447c5b4520560cd44672f2379905b889580d6754f1de9b279bae",
    strip_prefix = "rules_dotnet-0.0.5",
    urls = ["https://github.com/bazelbuild/rules_dotnet/archive/0.0.5.zip"],
    ## WORKAROUND: Force nuget2bazel to get missing libraries from nuget
    #patches = [
    #   "//:rules_dotnet_nuget2bazel_buffers.patch",
    #],
    #patch_args = ["-p1"],
)

load("@io_bazel_rules_dotnet//dotnet:deps.bzl", "dotnet_repositories")

dotnet_repositories()

load("@io_bazel_rules_dotnet//dotnet:defs.bzl", "core_register_sdk", "net_register_sdk", "mono_register_sdk",
    "dotnet_register_toolchains", "dotnet_repositories_nugets", "nuget_package")

dotnet_register_toolchains()
dotnet_repositories_nugets()

# For .NET Framework:
net_register_sdk(
    net_version = "net462",
    tools_version = "net462",
)

# (only useful for nuget2bazel)
core_register_sdk("v2.1.502", name = "core_sdk")


# bazel run @io_bazel_rules_dotnet//tools/nuget2bazel:nuget2bazel.exe -- add -l grpc 2.28.1 -p C:/path/to/rules_dotnet_memory_deps/
# bazel run @io_bazel_rules_dotnet//tools/nuget2bazel:nuget2bazel.exe -- add -l grpc.healthcheck 2.28.1 -p C:/path/to/rules_dotnet_memory_deps/
