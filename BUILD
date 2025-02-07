
package(default_visibility = ["//visibility:public"])

#load("@contrib_rules_jvm//docs:stardoc-input.bzl", "java_test_suite")
load("@contrib_rules_jvm//java:defs.bzl", "JUNIT5_DEPS", "java_test_suite")
load("@contrib_rules_jvm//docs:stardoc-input.bzl", "java_junit5_test")

java_library (
    name = "main",
    srcs = glob(["src/main/java/**/*.java"]),
    visibility = ["//visibility:public"],
    resources = ["src/main/resources"],
    deps = [
            "@maven//:jakarta_enterprise_jakarta_enterprise_cdi_api",
            "@maven//:jakarta_inject_jakarta_inject_api",
            "@maven//:jakarta_ws_rs_jakarta_ws_rs_api",
            "@maven//:io_rest_assured_rest_assured",
        ],
)
java_library(
    name = "resources",
    srcs = glob(["src/main/resources/**/*"]),
    resource_strip_prefix = "src/main/resources",
)
filegroup(
    name = "test_resources",
    srcs = glob(["src/main/resources/**"]),
    visibility = ["//visibility:public"],
)

java_junit5_test(
    name = "qtest",
    srcs = glob(["src/test/java/**/*.java"]),
    #resources = [":resources"],
    #resources = glob(["src/main/resources/**/*"]),
    resources = [":test_resources"],
    deps = [
        ":main",
        "@maven//:io_rest_assured_rest_assured",
        "@maven//:io_quarkus_quarkus_junit5",
        "@maven//:io_quarkus_quarkus_rest",
        "@maven//:org_junit_jupiter_junit_jupiter_api",
        "@maven//:org_junit_platform_junit_platform_reporting",
        "@maven//:org_junit_jupiter_junit_jupiter",

        "@maven//:io_quarkus_platform_quarkus_bom",
        "@maven//:io_quarkus_quarkus_bom",
        "@maven//:io_quarkus_quarkus_core",
        "@maven//:io_quarkus_quarkus_bootstrap_core",
    ],
    jvm_flags = [
            "-Dquarkus.test.profile=dev",
            "-Dquarkus.test.continuous-testing=disabled",
            "-Djava.util.logging.manager=org.jboss.logmanager.LogManager",
            "-Dquarkus.bootstrap.effective-model-builder=all",
            "-Dagentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005"
        ],
    #use_testrunner = True,
    test_class = "org.acme.getting.started.GreetingResourceTest",  # Replace with your test class name
    #main_class = "org.junit.platform.console.ConsoleLauncher",
)