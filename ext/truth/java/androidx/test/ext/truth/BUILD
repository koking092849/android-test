# Description: Build rules for building androidx.test.truth from source

load("@build_bazel_rules_android//android:rules.bzl", "android_library")
load("//build_extensions:release.bzl", "axt_release_lib")
load("//build_extensions:maven_repo.bzl", "maven_artifact")
load("//build_extensions:axt_versions.bzl", "ANDROIDX_ANNOTATION_VERSION", "ANDROIDX_TRUTH_VERSION", "ANNOTATION_VERSION", "CORE_VERSION", "GUAVA_VERSION", "TRUTH_VERSION")
load("//build_extensions:dackka_test.bzl", "dackka_test")
load("//build_extensions:api_checks.bzl", "api_checks")

# all users should reference the equivalent targets in //ext/truth
package(
    default_applicable_licenses = ["//:license"],
    default_visibility = [
        "//:__pkg__",
        "//ext/truth:__subpackages__",
    ],
)

licenses(["notice"])

android_library(
    name = "truth",
    testonly = 1,
    srcs = glob(
        ["**/*.java"],
    ),
    deps = [
        "//annotation",
        "//core",
        "@maven//:androidx_annotation_annotation",
        "@maven//:com_google_guava_guava",
        "@maven//:com_google_truth_truth",
    ],
)

# group of targets to use to produce release binary + docs
android_library(
    name = "truth_release_lib",
    testonly = 1,
    visibility = ["//visibility:private"],
    exports = [
        ":truth",
    ],
)

# Generate rules for the release artifacts. This generates three targets
# genrule output: truth_release_no_deps.jar and truth_release.aar
# a java_library target libtruth_release_no_deps
axt_release_lib(
    name = "truth_release",
    keep_spec = "androidx/test/ext/truth",
    remove_spec = "androidx/test/ext/truth/R[$$\\.]",
    deps = [
        ":truth_release_lib",
    ],
)

dackka_test(
    name = "truth_doc",
    jar = ":truth_release_all_deploy.jar",
    src_jar = ":libtruth-src.jar",
)

maven_artifact(
    name = "truth_maven_artifact",
    src = ":truth_release.aar",
    artifact_deps = [
        "androidx.test:core:%s" % CORE_VERSION,
        "com.google.guava:guava:%s" % GUAVA_VERSION,
        "com.google.truth:truth:%s" % TRUTH_VERSION,
        "androidx.annotation:annotation:%s" % ANDROIDX_ANNOTATION_VERSION,
        "androidx.test:annotation:%s" % ANNOTATION_VERSION,
    ],
    artifact_id = "truth",
    group_id = "androidx.test.ext",
    last_updated = "20180321000000",
    src_jar = ":libtruth-src.jar",
    version = "%s" % ANDROIDX_TRUTH_VERSION,
)

api_checks(
    name = "truth_api",
    deploy_jar = ":truth_release_all_deploy.jar",
    src_jar = ":libtruth-src.jar",
)
