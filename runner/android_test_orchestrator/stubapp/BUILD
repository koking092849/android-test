load("@build_bazel_rules_android//android:rules.bzl", "android_binary")
load("//build_extensions:maven_repo.bzl", "maven_artifact")
load("//build_extensions:axt_versions.bzl", "ORCHESTRATOR_VERSION", "SERVICES_VERSION")
load("//build_extensions:combine_jars.bzl", "combine_jars")

licenses(["notice"])

package(
    default_applicable_licenses = ["//:license"],
    default_visibility = ["//:__subpackages__"],
)

# Dummy app to allow the On Device Orchestration to run and execute.
android_binary(
    name = "stubapp",
    srcs = ["src/androidx/test/orchestrator/Orchestrator.java"],
    custom_package = "androidx.test.orchestrator.stubapp",
    manifest = "src/AndroidManifest.xml",
    multidex = "native",  # actually fits into one file, so skip main dex list
    proguard_specs = [
        "//:proguard_binary.cfg",
        "proguard_binary.cfg",
    ],
    visibility = ["//visibility:public"],
    deps = [
        "//runner/android_junit_runner",
        "//runner/android_test_orchestrator",
        "@maven//:androidx_multidex_multidex",
        "@maven//:com_google_guava_guava",
        "@maven//:junit_junit",
    ],
)

combine_jars(
    name = "orchestrator_src_jars",
    srcs = [
        "//runner/android_test_orchestrator/java/androidx/test/orchestrator:orchestrator_src",
    ],
)

maven_artifact(
    name = "orchestrator_release_maven_artifact",
    src = ":stubapp.apk",
    artifact_deps = [
        "androidx.test.services:test-services:%s" % SERVICES_VERSION,
    ],
    artifact_id = "orchestrator",
    group_id = "androidx.test",
    last_updated = "20170622000000",
    src_jar = ":orchestrator_src_jars.jar",
    version = "%s" % ORCHESTRATOR_VERSION,
)
