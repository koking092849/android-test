# Description:
#  Remote package for espresso.

load("@build_bazel_rules_android//android:rules.bzl", "android_library")
load("//build_extensions:maven_repo.bzl", "maven_artifact")
load("//build_extensions:axt_versions.bzl", "ANDROIDX_ANNOTATION_VERSION", "ESPRESSO_VERSION", "RUNNER_VERSION")
load("//build_extensions:dackka_test.bzl", "dackka_test")
load("//build_extensions:combine_jars.bzl", "combine_jars")
load("//build_extensions:release.bzl", "axt_release_lib")
load("//build_extensions:api_checks.bzl", "api_checks")

licenses(["notice"])

package(
    default_applicable_licenses = ["//espresso:license"],
    default_visibility = ["//:__subpackages__"],
)

COMMON_JAVACOPTS = [
    "-Xep:ObjectToString:OFF",  # See http://go/objecttostring-lsc
]

REMOTE_REGISTRY = [
    "RemoteDescriptorRegistry.java",
    "RemoteDescriptor.java",
    "FieldDescriptor.java",
]

android_library(
    name = "registry",
    srcs = REMOTE_REGISTRY,
    visibility = ["//visibility:public"],
    deps = [
        "//espresso/core/java/androidx/test/espresso/proto:ui_interaction_android_pb3",
        "//espresso/core/java/androidx/test/espresso/remote:exceptions",
        "//espresso/core/java/androidx/test/espresso/remote:reflectionUtils",
        "//espresso/core/java/androidx/test/espresso/remote/annotation:remote_msg_annotations",
        "//espresso/core/java/androidx/test/espresso/util",
        "//runner/monitor",
        "@com_google_protobuf//:protobuf_javalite",
        "@maven//:androidx_annotation_annotation",
        "@maven//:org_jetbrains_kotlin_kotlin_stdlib",
    ],
)

PROTO_UTILS = [
    "Converter.java",
    "AnyToTypeConverter.java",
    "TypeToAnyConverter.java",
    "ByteStringToTypeConverter.java",
    "TypeToByteStringConverter.java",
    "ParcelableToByteStringConverter.java",
    "ByteStringToParcelableConverter.java",
    "TypeProtoConverters.java",
    "ProtoUtils.java",
    "InteractionRequest.java",
    "GenericRemoteMessage.java",
    "RemoteMessageSerializer.java",
    "RemoteMessageDeserializer.java",
    "BuilderReflector.java",
    "ProtoReflector.java",
]

android_library(
    name = "protoUtils",
    srcs = PROTO_UTILS,
    visibility = ["//visibility:public"],
    deps = [
        ":registry",
        "//espresso/core/java/androidx/test/espresso:framework",
        "//espresso/core/java/androidx/test/espresso:interface",
        "//espresso/core/java/androidx/test/espresso/proto:ui_interaction_android_pb3",
        "//espresso/core/java/androidx/test/espresso/remote:aidls",
        "//espresso/core/java/androidx/test/espresso/remote:exceptions",
        "//espresso/core/java/androidx/test/espresso/remote:interface",
        "//espresso/core/java/androidx/test/espresso/remote:reflectionUtils",
        "//espresso/core/java/androidx/test/espresso/remote/annotation:remote_msg_annotations",
        "//espresso/core/java/androidx/test/espresso/util",
        "//opensource:hamcrest",
        "//runner/android_junit_runner",
        "@com_google_protobuf//:protobuf_javalite",
        "@maven//:androidx_annotation_annotation",
        "@maven//:org_jetbrains_kotlin_kotlin_stdlib",
    ],
)

android_library(
    name = "remote",
    srcs = glob(
        ["*.java"],
        exclude = PROTO_UTILS,
    ),
    javacopts = COMMON_JAVACOPTS,
    visibility = ["//visibility:public"],
    deps = [
        ":protoUtils",
        "//espresso/core/java/androidx/test/espresso",
        "//espresso/core/java/androidx/test/espresso:interface",
        "//espresso/core/java/androidx/test/espresso/matcher",
        "//espresso/core/java/androidx/test/espresso/proto:ui_interaction_android_pb3",
        "//espresso/core/java/androidx/test/espresso/proto/matcher:ui_interaction_view_matchers_android_pb3",
        "//espresso/core/java/androidx/test/espresso/remote:aidls",
        "//espresso/core/java/androidx/test/espresso/remote:bindable",
        "//espresso/core/java/androidx/test/espresso/remote:exceptions",
        "//espresso/core/java/androidx/test/espresso/remote:interface",
        "//espresso/core/java/androidx/test/espresso/remote:reflectionUtils",
        "//espresso/core/java/androidx/test/espresso/remote/annotation:remote_msg_annotations",
        "//espresso/remote/java/androidx/test/espresso:data-interaction-remote",
        "//espresso/remote/java/androidx/test/espresso/action:remote_view_actions",
        "//espresso/remote/java/androidx/test/espresso/assertion:remote_view_assertions",
        "//espresso/remote/java/androidx/test/espresso/matcher:remote_hamcrest_v1_3_core_matchers",
        "//espresso/remote/java/androidx/test/espresso/matcher:remote_view_matchers",
        "//espresso/remote/java/androidx/test/espresso/web/action:remote_web_actions",
        "//espresso/remote/java/androidx/test/espresso/web/assertion:remote_web_assertions",
        "//espresso/remote/java/androidx/test/espresso/web/matcher:remote_web_matchers",
        "//espresso/remote/java/androidx/test/espresso/web/model:remote_web_model_atoms",
        "//espresso/remote/java/androidx/test/espresso/web/sugar:remote_sugar",
        "//espresso/remote/java/androidx/test/espresso/web/webdriver:remote_webdriver_atoms",
        "//runner/android_junit_runner",
        "@com_google_protobuf//:protobuf_javalite",
        "@maven//:androidx_annotation_annotation",
        "@maven//:org_hamcrest_hamcrest_core",
        "@maven//:org_jetbrains_kotlin_kotlin_stdlib",
    ],
)

filegroup(
    name = "espresso_remote_src",
    srcs = [
        ":libprotoUtils-src.jar",
        ":libregistry-src.jar",
        ":libremote-src.jar",
    ],
)

combine_jars(
    name = "espresso_remote_src_jars",
    srcs = [
        ":espresso_remote_src",
    ],
)

axt_release_lib(
    name = "espresso_remote_release",
    jarjar_rules = ["release_jarjar_rules.txt"],
    keep_spec = "androidx/test/espresso",
    overlapping_jars = [
        "//espresso/core/java/androidx/test/espresso:espresso_core_release_no_deps.jar",
        "//espresso/web/java/androidx/test/espresso/web:espresso_web_release_no_deps.jar",
        "//espresso/idling_resource/java/androidx/test/espresso:espresso_idling_resource_release_no_deps.jar",
    ],
    proguard_library = ":proguard_library.cfg",
    proguard_specs = [
        "//:proguard_binary.cfg",
        "//espresso:proguard_binary.cfg",
    ],
    remove_spec = "androidx/test/espresso/remote/R[$$\\.]",
    deps = [
        ":remote",
    ],
)

dackka_test(
    name = "espresso_remote_doc",
    jar = ":espresso_remote_release_all_deploy.jar",
    src_jar = ":espresso_remote_src_jars.jar",
)

maven_artifact(
    name = "espresso_remote_maven_artifact",
    src = ":espresso_remote_release.aar",
    artifact_deps = [
        "androidx.test:runner:%s" % RUNNER_VERSION,
        "androidx.test.espresso:espresso-core:%s" % ESPRESSO_VERSION,
        "androidx.test.espresso:espresso-web:%s" % ESPRESSO_VERSION,
        "androidx.annotation:annotation:%s" % ANDROIDX_ANNOTATION_VERSION,
    ],
    artifact_id = "espresso-remote",
    group_id = "androidx.test.espresso",
    last_updated = "20170622000000",
    src_jar = ":espresso_remote_src_jars.jar",
    version = "%s" % ESPRESSO_VERSION,
)

api_checks(
    name = "espresso_remote_api",
    deploy_jar = ":espresso_remote_release_all_deploy.jar",
    src_jar = ":espresso_remote_src_jars.jar",
)
