load("@build_bazel_rules_android//android:rules.bzl", "android_library")

package(
    default_applicable_licenses = ["//espresso:license"],
    default_visibility = ["//visibility:public"],
)

licenses(["notice"])

REMOTE_WEB_MATCHERS = [
    "RemoteWebMatchers.java",
]

android_library(
    name = "remote_web_matchers",
    srcs = glob(
        REMOTE_WEB_MATCHERS,
    ),
    deps = [
        "//espresso/core/java/androidx/test/espresso/remote:exceptions",
        "//espresso/core/java/androidx/test/espresso/remote:interface",
        "//espresso/core/java/androidx/test/espresso/remote:reflectionUtils",
        "//espresso/remote/java/androidx/test/espresso/remote:protoUtils",
        "//espresso/remote/java/androidx/test/espresso/remote:registry",
        "//espresso/remote/java/androidx/test/espresso/web/proto/matcher:remote_web_matchers_proto_android_pb3",
        "//espresso/web/java/androidx/test/espresso/web/matcher",
    ],
)
