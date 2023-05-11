# https://github.com/bazelbuild/rules_jvm_external#usage
# switch to https://github.com/bazelbuild/rules_jvm_external/blob/master/docs/bzlmod.md ?
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

RULES_JVM_EXTERNAL_TAG = "5.2"
RULES_JVM_EXTERNAL_SHA ="f86fd42a809e1871ca0aabe89db0d440451219c3ce46c58da240c7dcdc00125f"

http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    url = "https://github.com/bazelbuild/rules_jvm_external/releases/download/%s/rules_jvm_external-%s.tar.gz" % (RULES_JVM_EXTERNAL_TAG, RULES_JVM_EXTERNAL_TAG)
)

load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")

rules_jvm_external_deps()

load("@rules_jvm_external//:setup.bzl", "rules_jvm_external_setup")

rules_jvm_external_setup()

load("@rules_jvm_external//:defs.bzl", "maven_install")

load("@rules_jvm_external//:defs.bzl", "artifact")
load("@rules_jvm_external//:specs.bzl", "maven")

maven_install(
    artifacts = [
        maven.artifact("org.junit.jupiter", "junit-jupiter", "5.9.3", testonly = True),
        maven.artifact("org.junit.platform", "junit-platform-console-standalone", "1.9.3", testonly = True),

    ],
    repositories = [
        "https://repo1.maven.org/maven2",
        "https://search.maven.org/",
        "https://repo.maven.apache.org/maven2/",
    ],
    maven_install_json = "@//:maven_install.json",
    fetch_sources = True,
)

load("@maven//:defs.bzl", "pinned_maven_install")
pinned_maven_install()
