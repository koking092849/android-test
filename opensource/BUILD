load("@build_bazel_rules_android//android:rules.bzl", "android_library")

# aliases that creates bazel targets that are equivalent to blaze

android_library(
    name = "hamcrest",
    visibility = [
        "//visibility:public",
    ],
    exports = [
        "@maven//:org_hamcrest_hamcrest_core",
        "@maven//:org_hamcrest_hamcrest_library",
    ],
)

java_import(
    name = "androidsdk_compiletime",
    jars = [
        "@androidsdk//:platforms/android-33/android.jar",
    ],
    neverlink = 1,
    visibility = [
        "//visibility:public",
    ],
)
