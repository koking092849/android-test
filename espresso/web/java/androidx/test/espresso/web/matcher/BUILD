load("@build_bazel_rules_android//android:rules.bzl", "android_library")

package(
    default_applicable_licenses = ["//espresso:license"],
    default_visibility = ["//visibility:public"],
)

licenses(["notice"])

android_library(
    name = "matcher",
    srcs = glob(
        ["*.java"],
    ),
    exports = [
        "//opensource:hamcrest",
    ],
    deps = [
        "//espresso/core/java/androidx/test/espresso:interface",
        "//espresso/core/java/androidx/test/espresso/matcher",
        "//espresso/core/java/androidx/test/espresso/remote/annotation:remote_msg_annotations",
        "//espresso/web/java/androidx/test/espresso/web/internal/bridge",
        "//opensource:hamcrest",
        "//runner/monitor",
        "@maven//:androidx_annotation_annotation",
    ],
)
