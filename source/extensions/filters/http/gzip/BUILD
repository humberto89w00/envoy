load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_extension",
    "envoy_cc_library",
    "envoy_extension_package",
)

licenses(["notice"])  # Apache 2

# HTTP L7 filter that performs gzip compression
# Public docs: docs/root/configuration/http_filters/gzip_filter.rst

envoy_extension_package()

envoy_cc_library(
    name = "gzip_filter_lib",
    srcs = ["gzip_filter.cc"],
    hdrs = ["gzip_filter.h"],
    deps = [
        "//source/common/http:headers_lib",
        "//source/common/protobuf",
        "//source/extensions/compression/gzip/compressor:compressor_lib",
        "//source/extensions/filters/http/common/compressor:compressor_lib",
        "@envoy_api//envoy/config/core/v3:pkg_cc_proto",
        "@envoy_api//envoy/extensions/filters/http/gzip/v3:pkg_cc_proto",
    ],
)

envoy_cc_extension(
    name = "config",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    security_posture = "robust_to_untrusted_downstream",
    deps = [
        "//source/extensions/filters/http:well_known_names",
        "//source/extensions/filters/http/common:factory_base_lib",
        "//source/extensions/filters/http/gzip:gzip_filter_lib",
        "@envoy_api//envoy/extensions/filters/http/gzip/v3:pkg_cc_proto",
    ],
)
