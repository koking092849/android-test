load("//build_extensions:axt_android_local_test.bzl", "axt_android_local_test")

package(default_applicable_licenses = ["//:license"])

# Description: Tests for the Orchestrator client connection
licenses(["notice"])

axt_android_local_test(
    name = "OrchestrationListenerManagerTest",
    size = "small",
    srcs = [
        "OrchestrationListenerManagerTest.java",
    ],
    deps = [
        "//opensource:hamcrest",
        "//runner/android_junit_runner",
        "//runner/android_junit_runner/javatests/androidx/test/orchestrator:sample_junit_test",
        "//services/events/java/androidx/test/services/events",
        "@maven//:junit_junit",
        "@maven//:org_mockito_mockito_core",
    ],
)
