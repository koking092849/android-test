# Protocol buffer definitions for remote web actions

licenses(["notice"])

package(
    default_applicable_licenses = ["//espresso:license"],
    default_visibility = [
        "//espresso/core/java/androidx/test/espresso:espresso_pkg",
        "//espresso/web/java/androidx/test/espresso/web/action:__pkg__",
    ],
)

proto_library(
    name = "web_actions_proto",
    srcs = ["web_actions.proto"],
    deps = [
        "@com_google_protobuf//:any_proto",
    ],
)

java_lite_proto_library(
    name = "web_actions_proto_android_pb3",
    deps = [":web_actions_proto"],
)
