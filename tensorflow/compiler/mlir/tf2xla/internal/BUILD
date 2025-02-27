load("//tensorflow/core/platform:rules_cc.bzl", "cc_library")
load("//tensorflow:tensorflow.bzl", "tf_cc_test")

package(
    # copybara:uncomment default_applicable_licenses = ["//tensorflow:license"],
    default_visibility = [
        "//tensorflow/compiler/mlir/tf2xla/api/v0:__subpackages__",
        "//tensorflow/compiler/mlir/tf2xla/api/v1:__subpackages__",
    ],
)

cc_library(
    name = "mlir_pass_instrumentation",
    srcs = ["mlir_pass_instrumentation.cc"],
    hdrs = ["mlir_pass_instrumentation.h"],
    deps = [
        "//tensorflow/core/platform:logging",
        "@llvm-project//mlir:Pass",
    ],
)

tf_cc_test(
    name = "mlir_pass_instrumentation_test",
    srcs = ["mlir_pass_instrumentation_test.cc"],
    deps = [
        ":mlir_pass_instrumentation",
        "//tensorflow/compiler/mlir/tf2xla/api/v0:compile_mlir_util_no_tf_dialect_passes",
        "//tensorflow/core:test",
        "@com_google_googletest//:gtest_main",
    ],
)

cc_library(
    name = "legalize_tf_mlir",
    srcs = ["legalize_tf_mlir.cc"],
    hdrs = ["legalize_tf_mlir.h"],
    deps = [
        "//tensorflow/compiler/mlir/tensorflow",
        "//tensorflow/compiler/mlir/tensorflow:serialize_mlir_module_utils",
        "//tensorflow/compiler/mlir/tensorflow/transforms:set_tpu_infeed_layout",
        "//tensorflow/compiler/mlir/tf2xla:compile_mlir_util",
        "//tensorflow/compiler/tf2xla:layout_util",
        "//tensorflow/compiler/tf2xla:xla_compiler",
        "//tensorflow/compiler/tf2xla:xla_helpers",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla/mlir_hlo:hlo_dialect_registration",
        "//tensorflow/core:framework",
        "//tensorflow/core:lib",
        "//tensorflow/core/protobuf/tpu:compile_metadata_proto_cc",
        "//tensorflow/core/tpu:tpu_compile",
        "//tensorflow/core/tpu/kernels:tpu_compile_op_support",
        "//tensorflow/tsl/platform:error_logging",
        "//tensorflow/tsl/platform:statusor",
        "@com_google_absl//absl/log",
        "@llvm-project//llvm:Support",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:Pass",
        "@stablehlo//:register",
    ],
)

cc_library(
    name = "legalize_tf_to_hlo",
    srcs = ["legalize_tf_to_hlo.cc"],
    hdrs = ["legalize_tf_to_hlo.h"],
    deps = [
        ":legalize_tf_mlir",
        "//tensorflow/compiler/mlir/tf2xla/api/v0:compile_tf_graph",
        "//tensorflow/compiler/tf2xla:layout_util",
        "//tensorflow/compiler/tf2xla:xla_helpers",
        "//tensorflow/compiler/tf2xla:xla_tpu_backend_registration",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla/client:compile_only_client",
        "//tensorflow/core:framework",
        "//tensorflow/core/platform:status",
        "//tensorflow/core/protobuf/tpu:compile_metadata_proto_cc",
        "//tensorflow/core/tpu/kernels:tpu_compile_op_support",
        "//tensorflow/tsl/platform:statusor",
        "@llvm-project//llvm:Support",
        "@llvm-project//mlir:Pass",
    ],
)

tf_cc_test(
    name = "legalize_tf_mlir_test",
    srcs = ["legalize_tf_mlir_test.cc"],
    deps = [
        ":legalize_tf_mlir",
        "//tensorflow/compiler/jit",
        "//tensorflow/compiler/mlir/tf2xla:compile_mlir_util",
        "//tensorflow/compiler/tf2xla:xla_compiler",
        "//tensorflow/compiler/tf2xla:xla_helpers",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/core:framework",
        "//tensorflow/core:test_main",
        "//tensorflow/core/lib/monitoring:cell_reader",
        "//tensorflow/core/protobuf/tpu:compile_metadata_proto_cc",
        "//tensorflow/core/tpu/kernels:tpu_compile_op_support",
        "//tensorflow/tsl/platform:statusor",
        "@com_google_googletest//:gtest",
        "@llvm-project//mlir:Pass",
    ],
)

tf_cc_test(
    name = "legalize_tf_to_hlo_test",
    srcs = ["legalize_tf_to_hlo_test.cc"],
    deps = [
        ":legalize_tf_to_hlo",
        "//tensorflow/compiler/jit",
        "//tensorflow/compiler/mlir/tf2xla:compile_mlir_util",
        "//tensorflow/compiler/tf2xla:xla_compiler",
        "//tensorflow/compiler/tf2xla:xla_helpers",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/compiler/xla/client:client_library",
        "//tensorflow/compiler/xla/stream_executor",
        "//tensorflow/core:framework",
        "//tensorflow/core:protos_all_cc",
        "//tensorflow/core:test_main",
        "//tensorflow/core/lib/monitoring:cell_reader",
        "//tensorflow/core/protobuf:for_core_protos_cc",
        "//tensorflow/core/protobuf/tpu:compile_metadata_proto_cc",
        "//tensorflow/core/tpu/kernels:tpu_compile_op_support",
        "//tensorflow/tsl/platform:statusor",
        "@com_google_googletest//:gtest",
        "@llvm-project//mlir:Pass",
    ],
)
