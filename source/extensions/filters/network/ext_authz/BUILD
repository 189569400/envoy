load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_extension",
    "envoy_cc_library",
    "envoy_extension_package",
)

licenses(["notice"])  # Apache 2

# External authorization L4 network filter
# Public docs: TODO(saumoh): Docs needed in docs/root/configuration/listeners/network_filters

envoy_extension_package()

envoy_cc_library(
    name = "ext_authz",
    srcs = ["ext_authz.cc"],
    hdrs = ["ext_authz.h"],
    deps = [
        "//envoy/network:connection_interface",
        "//envoy/network:filter_interface",
        "//envoy/runtime:runtime_interface",
        "//envoy/stats:stats_macros",
        "//envoy/upstream:cluster_manager_interface",
        "//source/common/common:assert_lib",
        "//source/common/common:matchers_lib",
        "//source/common/tracing:http_tracer_lib",
        "//source/extensions/filters/common/ext_authz:ext_authz_grpc_lib",
        "//source/extensions/filters/common/ext_authz:ext_authz_interface",
        "//source/extensions/filters/network:well_known_names",
        "@envoy_api//envoy/extensions/filters/network/ext_authz/v3:pkg_cc_proto",
        "@envoy_api//envoy/service/auth/v3:pkg_cc_proto",
    ],
)

envoy_cc_extension(
    name = "config",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    deps = [
        "//envoy/registry",
        "//source/common/config:utility_lib",
        "//source/common/protobuf:utility_lib",
        "//source/extensions/filters/network:well_known_names",
        "//source/extensions/filters/network/common:factory_base_lib",
        "//source/extensions/filters/network/ext_authz",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/extensions/filters/network/ext_authz/v3:pkg_cc_proto",
    ],
)
