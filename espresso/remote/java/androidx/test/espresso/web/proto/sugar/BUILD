# Protocol buffer definitions for remote web sugar atoms

licenses(["notice"])

package(
    default_applicable_licenses = ["//espresso:license"],
    default_visibility = [
        "//espresso/core/java/androidx/test/espresso:espresso_pkg",
        "//espresso/web/java/androidx/test/espresso/web/sugar:__pkg__",
    ],
)

proto_library(
    name = "web_sugar_proto",
    srcs = ["web_sugar.proto"],
    deps = [
        "@com_google_protobuf//:any_proto",
    ],
)

java_lite_proto_library(
    name = "web_sugar_proto_android_pb3",
    deps = [":web_sugar_proto"],
)
