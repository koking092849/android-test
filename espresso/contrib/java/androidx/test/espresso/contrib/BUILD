load("@build_bazel_rules_android//android:rules.bzl", "android_library")
load("//build_extensions:release.bzl", "axt_release_lib")
load("//build_extensions:maven_repo.bzl", "maven_artifact")
load(
    "//build_extensions:axt_versions.bzl",
    "ANDROIDX_CORE_VERSION",
    "ANDROIDX_DRAWER_LAYOUT_VERSION",
    "ANDROIDX_LEGACY_SUPPORT_VERSION",
    "ANDROIDX_RECYCLERVIEW_VERSION",
    "ANDROIDX_VIEWPAGER_VERSION",
    "ATF_VERSION",
    "ESPRESSO_VERSION",
    "GOOGLE_MATERIAL_VERSION",
)
load("//build_extensions:combine_jars.bzl", "combine_jars")
load("//build_extensions:dackka_test.bzl", "dackka_test")
load("//build_extensions:api_checks.bzl", "api_checks")

# Description:
#   Contributed / non-core functionality of Espresso. Tools which add on to
#   Espresso belong here.
licenses(["notice"])

package(
    default_applicable_licenses = ["//espresso:license"],
    default_visibility = ["//:__subpackages__"],
)

COMMON_JAVACOPTS = [
    "-Xep:ObjectToString:OFF",  # See http://go/objecttostring-lsc
]

android_library(
    name = "resources",
    manifest = "AndroidManifest.xml",
    resource_files = glob(["res/**"]),
)

android_library(
    name = "counting_idling_resource",
    visibility = ["//visibility:public"],
    exports = [
        "//espresso/idling_resource/java/androidx/test/espresso:counting_idling_resource",
    ],
)

android_library(
    name = "scheduled_thread_pool_idling_resource",
    visibility = ["//visibility:public"],
    exports = [
        "//espresso/idling_resource/concurrent/java/androidx/test/espresso/idling/concurrent:scheduled_thread_pool_idling_resource",
    ],
)

android_library(
    name = "thread_pool_idling_resource",
    visibility = ["//visibility:public"],
    exports = [
        "//espresso/idling_resource/concurrent/java/androidx/test/espresso/idling/concurrent:thread_pool_idling_resource",
    ],
)

android_library(
    name = "picker_actions",
    srcs = ["PickerActions.java"],
    visibility = ["//visibility:public"],
    deps = [
        "//espresso/core/java/androidx/test/espresso",
        "//espresso/core/java/androidx/test/espresso:framework",
        "//espresso/core/java/androidx/test/espresso:interface",
        "//espresso/core/java/androidx/test/espresso/matcher",
        "//opensource:hamcrest",
    ],
)

COMMON_JAVACOPTS = [
    "-Xep:ObjectToString:OFF",  # See http://go/objecttostring-lsc
]

android_library(
    name = "recycler_view",
    srcs = ["RecyclerViewActions.java"],
    javacopts = COMMON_JAVACOPTS,
    visibility = ["//visibility:public"],
    deps = [
        "//espresso/core/java/androidx/test/espresso",
        "//espresso/core/java/androidx/test/espresso/matcher",
        "//opensource:hamcrest",
        "//runner/monitor",
        "@maven//:androidx_recyclerview_recyclerview",
    ],
)

android_library(
    name = "drawer_actions",
    testonly = 1,
    srcs = [
        "DrawerActions.java",
        "DrawerMatchers.java",
    ],
    visibility = ["//visibility:public"],
    deps = [
        ":resources",
        "//espresso/core/java/androidx/test/espresso",
        "//espresso/core/java/androidx/test/espresso/matcher",
        "//opensource:hamcrest",
        "@maven//:androidx_core_core",
        "@maven//:androidx_drawerlayout_drawerlayout",
    ],
)

android_library(
    name = "activity_result_matchers",
    srcs = [
        "ActivityResultMatchers.java",
    ],
    visibility = ["//visibility:public"],
    deps = [
        "//opensource:hamcrest",
    ],
)

android_library(
    name = "accessibility_checks",
    testonly = 1,
    srcs = [
        "AccessibilityChecks.java",
    ],
    visibility = ["//visibility:public"],
    deps = [
        "//espresso/core/java/androidx/test/espresso",
        "//opensource:hamcrest",
        "@maven//:com_google_android_apps_common_testing_accessibility_framework_accessibility_test_framework",
    ],
)

android_library(
    name = "design_lib_actions",
    testonly = 1,
    srcs = ["NavigationViewActions.java"],
    visibility = ["//visibility:public"],
    deps = [
        "//espresso/core/java/androidx/test/espresso",
        "//espresso/core/java/androidx/test/espresso/matcher",
        "//opensource:hamcrest",
        "@maven//:androidx_appcompat_appcompat",
        "@maven//:androidx_drawerlayout_drawerlayout",
        "@maven//:com_google_android_material_material",
    ],
)

android_library(
    name = "view_pager_actions",
    testonly = 1,
    srcs = ["ViewPagerActions.java"],
    visibility = ["//visibility:public"],
    deps = [
        "//espresso/core/java/androidx/test/espresso",
        "//espresso/core/java/androidx/test/espresso/action",
        "//espresso/core/java/androidx/test/espresso/matcher",
        "//opensource:hamcrest",
        "@maven//:androidx_viewpager_viewpager",
    ],
)

android_library(
    name = "espresso_contrib_release_lib",
    testonly = 1,
    exports = [
        ":accessibility_checks",
        ":activity_result_matchers",
        ":design_lib_actions",
        ":drawer_actions",
        ":picker_actions",
        ":recycler_view",
        ":view_pager_actions",
    ],
)

axt_release_lib(
    name = "espresso_contrib_release",
    keep_spec = "androidx/test/espresso/contrib",
    multidex = "native",
    remove_spec = "androidx/test/espresso/contrib/R[$$\\.]",
    resource_files = glob(["res/**"]),
    deps = [
        ":espresso_contrib_release_lib",
    ],
)

filegroup(
    name = "contrib_src",
    srcs = [
        ":libaccessibility_checks-src.jar",
        ":libactivity_result_matchers-src.jar",
        ":libcounting_idling_resource-src.jar",
        ":libdesign_lib_actions-src.jar",
        ":libdrawer_actions-src.jar",
        ":libpicker_actions-src.jar",
        ":librecycler_view-src.jar",
        ":libview_pager_actions-src.jar",
    ],
)

combine_jars(
    name = "contrib_src_jars",
    srcs = [
        ":contrib_src",
    ],
)

dackka_test(
    name = "espresso_contrib_doc",
    jar = ":espresso_contrib_release_all_deploy.jar",
    src_jar = ":contrib_src_jars.jar",
)

maven_artifact(
    name = "espresso_contrib_maven_artifact",
    src = ":espresso_contrib_release.aar",
    artifact_deps = [
        "androidx.test.espresso:espresso-core:%s" % ESPRESSO_VERSION,
        "androidx.test.espresso:espresso-idling-resource:%s" % ESPRESSO_VERSION,
        "com.google.android.material:material:%s" % GOOGLE_MATERIAL_VERSION,
        "androidx.recyclerview:recyclerview:%s" % ANDROIDX_RECYCLERVIEW_VERSION,
        "androidx.drawerlayout:drawerlayout:%s" % ANDROIDX_DRAWER_LAYOUT_VERSION,
        "androidx.viewpager:viewpager:%s" % ANDROIDX_VIEWPAGER_VERSION,
        "androidx.core:core:%s" % ANDROIDX_CORE_VERSION,
        "androidx.legacy:legacy-support-core-utils:%s" % ANDROIDX_LEGACY_SUPPORT_VERSION,
        "com.google.android.apps.common.testing.accessibility.framework:accessibility-test-framework:%s" % ATF_VERSION,
    ],
    artifact_id = "espresso-contrib",
    group_id = "androidx.test.espresso",
    last_updated = "20170622000000",
    src_jar = ":contrib_src_jars.jar",
    version = "%s" % ESPRESSO_VERSION,
)

api_checks(
    name = "espresso_contrib_api",
    deploy_jar = ":espresso_contrib_release_all_deploy.jar",
    src_jar = ":contrib_src_jars.jar",
)
