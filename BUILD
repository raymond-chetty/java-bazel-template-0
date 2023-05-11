lib_deps = [

]

main_deps = [

]

test_deps = [
      "@maven//:org_junit_jupiter_junit_jupiter",
      "@maven//:org_junit_jupiter_junit_jupiter_api",
      "@maven//:org_junit_platform_junit_platform_console_standalone",
]

java_library(
    name = "Lib",
    srcs = glob([
        "src/lib/*.java",
        "src/lib/**/*.java",
    ]),
    deps = lib_deps,
    runtime_deps = [],
)

java_binary(
    name = "Main",
    srcs = glob([
        "src/main/*.java",
        "src/main/**/*.java",
    ]),
    deps = [
        "//:Lib",
      ] + lib_deps + main_deps,
    runtime_deps = [],
    main_class = "com.github.yarloocll.template0.Main",
    resources = glob([
        "src/main/resources/*",
        "src/main/resources/**/*",
        "src/main/META-INF/*",
        "src/main/META-INF/**/*",
    ]),
    resource_strip_prefix = "src/main/"
)

java_test(
    name = "LibTests",
    srcs = glob([
      "src/test/*.java",
      "src/test/**/*.java",
      
      "src/main/logging/*.java",
    ]),
    deps = [
        "//:Lib",
      ] + lib_deps + main_deps + test_deps,
    runtime_deps = [],
    main_class = "org.junit.platform.console.ConsoleLauncher",
    args = ["--select-package=com.github.yarloocll"],
    use_testrunner = False,
    timeout = "short",
)
