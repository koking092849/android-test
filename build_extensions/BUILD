load("@bazel_skylib//:bzl_library.bzl", "bzl_library")

licenses(["notice"])

package(default_visibility = [
    "//visibility:public",
])

filegroup(
    name = "bzl",
    srcs = [
        "add_or_update_file_in_zip.bzl",
        "combine_jars.bzl",
        "maven_repo.bzl",
        "release.bzl",
        "remove_from_jar.bzl",
    ],
)

# Used to generate a maven repository.
py_binary(
    name = "maven_repository",
    srcs = ["maven_repository.py"],
    deps = [
        "@absl_py//absl:app",
        "@absl_py//absl/flags",
    ],
)

# Used to generate a maven artifact.
sh_binary(
    name = "maven_artifact",
    srcs = ["maven_artifact.sh"],
)

exports_files([
    "noJarJarRules.txt",
    "AndroidManifest_target_stub.xml",
    "AndroidManifest_instrumentation_test_template.xml",
    "AndroidManifest_robolectric.xml",
    "robolectric.properties",
])

bzl_library(
    name = "remove_from_jar_lib",
    srcs = ["remove_from_jar.bzl"],
)
