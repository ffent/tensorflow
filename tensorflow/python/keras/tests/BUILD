# Description:
#   Contains Keras test utils and integration tests.

load("//tensorflow:tensorflow.bzl", "cuda_py_test")

# buildifier: disable=same-origin-load
load("//tensorflow:tensorflow.bzl", "tf_py_test")
load("//tensorflow/python/tpu:tpu.bzl", "tpu_py_test")
load("//tensorflow/compiler/tests:build_defs.bzl", "tf_xla_py_test")

package(
    default_visibility = [
        "//tensorflow/tools/pip_package:__pkg__",
    ],
    licenses = ["notice"],  # Apache 2.0
)

exports_files(["LICENSE"])

filegroup(
    name = "all_py_srcs",
    srcs = glob(["*.py"]),
    visibility = ["//tensorflow/python/keras/google/private_tf_api_test:__pkg__"],
)

tf_py_test(
    name = "get_config_test",
    srcs = ["get_config_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = [
        "no_pip",
    ],
    tfrt_enabled = True,
    deps = [
        ":get_config_samples",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python/keras",
        "@absl_py//absl/testing:parameterized",
    ],
)

tf_py_test(
    name = "add_loss_correctness_test",
    srcs = ["add_loss_correctness_test.py"],
    python_version = "PY3",
    shard_count = 4,
    deps = [
        "//tensorflow/python:client_testlib",
        "//tensorflow/python/keras",
        "//third_party/py/numpy",
        "@absl_py//absl/testing:parameterized",
    ],
)

tpu_py_test(
    name = "automatic_outside_compilation_test",
    srcs = [
        "automatic_outside_compilation_test.py",
    ],
    disable_experimental = True,
    python_version = "PY3",
    tags = ["no_oss"],
    deps = [
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:config",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:errors",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:function",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:platform",
        "//tensorflow/python:random_ops",
        "//tensorflow/python:string_ops",
        "//tensorflow/python:summary",
        "//tensorflow/python:summary_ops_v2",
        "//tensorflow/python:training_lib",
        "//tensorflow/python:training_util",
        "//tensorflow/python:variables",
        "//tensorflow/python/eager:test",
        "//tensorflow/python/keras",
        "//tensorflow/python/keras/distribute:distribute_strategy_test_lib",
        "//tensorflow/python/ops/losses",
    ],
)

tf_py_test(
    name = "convert_to_constants_test",
    srcs = ["convert_to_constants_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tfrt_enabled = True,
    deps = [
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:convert_to_constants",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:init_ops",
        "//tensorflow/python:tensor_spec",
        "//tensorflow/python:util",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/saved_model:load",
        "//tensorflow/python/saved_model:save",
        "//tensorflow/python/training/tracking",
    ],
)

tf_py_test(
    name = "custom_training_loop_test",
    srcs = ["custom_training_loop_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = ["notsan"],
    deps = [
        "//tensorflow/python:client_testlib",
        "//tensorflow/python/keras",
        "//third_party/py/numpy",
        "@absl_py//absl/testing:parameterized",
    ],
)

tf_py_test(
    name = "graph_util_test",
    srcs = ["graph_util_test.py"],
    python_version = "PY3",
    tfrt_enabled = True,
    deps = [
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:graph_util",
        "//tensorflow/python:saver",
        "//tensorflow/python:session",
        "//tensorflow/python:tf_optimizer",
    ],
)

tf_py_test(
    name = "integration_test",
    size = "medium",
    srcs = ["integration_test.py"],
    python_version = "PY3",
    shard_count = 16,
    tags = [
        "no_rocm",
        "notsan",
    ],
    deps = [
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:nn_ops",
        "//tensorflow/python/keras",
        "//third_party/py/numpy",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "model_architectures",
    srcs = [
        "model_architectures.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/python/keras",
    ],
)

tf_py_test(
    name = "model_architectures_test",
    srcs = ["model_architectures_test.py"],
    python_version = "PY3",
    shard_count = 16,
    tfrt_enabled = True,
    deps = [
        ":model_architectures",
        "//tensorflow/python/keras",
        "//third_party/py/numpy",
        "@absl_py//absl/testing:parameterized",
    ],
)

py_library(
    name = "model_subclassing_test_util",
    srcs = ["model_subclassing_test_util.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/python/keras",
    ],
)

tf_py_test(
    name = "model_subclassing_test",
    srcs = ["model_subclassing_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = [
        "no_windows",
        "notsan",
    ],
    deps = [
        ":model_subclassing_test_util",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python/keras",
        "//tensorflow/python/keras:combinations",
        "//third_party/py/numpy",
        "@absl_py//absl/testing:parameterized",
    ],
)

tf_py_test(
    name = "model_subclassing_compiled_test",
    srcs = ["model_subclassing_compiled_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = [
        "no_windows",
        "notsan",
    ],
    deps = [
        ":model_subclassing_test_util",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python/keras",
        "//third_party/py/numpy",
        "@absl_py//absl/testing:parameterized",
    ],
)

cuda_py_test(
    name = "memory_test",
    size = "medium",
    srcs = ["memory_test.py"],
    tags = [
        "manual",
        "no_oss",
        "notap",  #TODO(b/140640597): this test is flaky at the moment
        "optonly",  # The test is too slow in non-opt mode
    ],
    # TODO(b/140065350): Re-enable
    xla_enable_strict_auto_jit = False,
    deps = [
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python/eager:backprop",
        "//tensorflow/python/eager:test",
        "//tensorflow/python/eager/memory_tests:memory_test_util",
        "//tensorflow/python/keras",
        "@six_archive//:six",
    ],
)

tf_py_test(
    name = "memory_checker_test",
    size = "medium",
    srcs = ["memory_checker_test.py"],
    python_version = "PY3",
    shard_count = 8,
    tags = [
        "no_oss",
        "no_pip",
        "no_windows",
        "noasan",  # TODO(b/149948895): Re-enable.
        "nomsan",  # TODO(b/149948895): Re-enable.
        "notsan",  # TODO(b/149948895): Re-enable.
    ],
    tfrt_enabled = True,
    deps = [
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:extra_py_tests_deps",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:memory_checker",
    ],
)

cuda_py_test(
    name = "op_callbacks_test",
    srcs = ["op_callbacks_test.py"],
    python_version = "PY3",
    xla_enable_strict_auto_jit = False,
    deps = [
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:op_callbacks",
        "//tensorflow/python:script_ops",
        "//tensorflow/python:util",
        "//tensorflow/python/eager:context",
        "//tensorflow/python/eager:test",
        "//tensorflow/python/keras:combinations",
    ],
)

cuda_py_test(
    name = "summary_ops_test",
    size = "small",
    srcs = ["summary_ops_test.py"],
    tfrt_enabled = True,
    deps = [
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:lib",
        "//tensorflow/python:platform",
        "//tensorflow/python:summary_ops_v2",
        "//tensorflow/python/keras/engine",
        "//tensorflow/python/keras/layers:core",
    ],
)

tf_py_test(
    name = "saved_model_test",
    size = "small",
    srcs = ["saved_model_test.py"],
    tfrt_enabled = True,
    deps = [
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:tensor_spec",
        "//tensorflow/python/eager:backprop",
        "//tensorflow/python/eager:function",
        "//tensorflow/python/keras/layers:core",
        "//tensorflow/python/keras/optimizer_v2",
        "//tensorflow/python/saved_model:save",
        "//tensorflow/python/training/tracking:util",
    ],
)

cuda_py_test(
    name = "saver_test",
    size = "medium",
    srcs = ["saver_test.py"],
    python_version = "PY3",
    deps = [
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:errors",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:nn_grad",
        "//tensorflow/python:resource_variable_ops",
        "//tensorflow/python:saver",
        "//tensorflow/python:training_lib",
        "//tensorflow/python:training_util",
        "//tensorflow/python/eager:context",
        "//tensorflow/python/keras/engine",
        "//tensorflow/python/keras/layers:core",
        "//tensorflow/python/training/tracking",
        "//tensorflow/python/training/tracking:util",
    ],
)

tf_py_test(
    name = "serialization_util_test",
    size = "small",
    srcs = ["serialization_util_test.py"],
    python_version = "PY3",
    tfrt_enabled = True,
    deps = [
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:util",
        "//tensorflow/python/keras:combinations",
        "//tensorflow/python/keras/engine",
        "//tensorflow/python/keras/layers:core",
    ],
)

tf_py_test(
    name = "temporal_sample_weights_correctness_test",
    srcs = ["temporal_sample_weights_correctness_test.py"],
    python_version = "PY3",
    shard_count = 20,
    deps = [
        "//tensorflow/python:client_testlib",
        "//tensorflow/python/keras",
        "//third_party/py/numpy",
    ],
)

tf_py_test(
    name = "tracking_test",
    srcs = ["tracking_test.py"],
    python_version = "PY3",
    tags = [
        "no_windows",
        "nomac",
    ],
    tfrt_enabled = True,
    deps = [
        "//tensorflow/python:array_ops",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:variables",
        "//tensorflow/python/eager:context",
        "//tensorflow/python/eager:test",
        "//tensorflow/python/keras:combinations",
        "//tensorflow/python/keras/engine",
        "//tensorflow/python/keras/layers:core",
        "//tensorflow/python/keras/layers:normalization",
        "//tensorflow/python/module",
        "//tensorflow/python/training/tracking",
        "//tensorflow/python/training/tracking:data_structures",
        "//tensorflow/python/training/tracking:util",
        "@absl_py//absl/testing:parameterized",
    ],
)

tf_py_test(
    name = "tracking_util_test",
    srcs = ["tracking_util_test.py"],
    python_version = "PY3",
    tags = ["notsan"],  # b/74395663
    tfrt_enabled = True,
    deps = [
        "//tensorflow/compiler/tests:xla_test",
        "//tensorflow/python:checkpoint_management",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:extra_py_tests_deps",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:init_ops",
        "//tensorflow/python:platform",
        "//tensorflow/python:resource_variable_ops",
        "//tensorflow/python:saver",
        "//tensorflow/python:state_ops",
        "//tensorflow/python:template",
        "//tensorflow/python:training_util",
        "//tensorflow/python:variable_scope",
        "//tensorflow/python:variables",
        "//tensorflow/python/eager:backprop",
        "//tensorflow/python/eager:context",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/keras:combinations",
        "//tensorflow/python/keras/engine",
        "//tensorflow/python/keras/layers:core",
        "//tensorflow/python/keras/optimizer_v2",
        "//tensorflow/python/training/tracking",
        "//tensorflow/python/training/tracking:graph_view",
        "//tensorflow/python/training/tracking:util",
        "@absl_py//absl/testing:parameterized",
    ],
)

tf_py_test(
    name = "tracking_util_with_v1_optimizers_test",
    srcs = ["tracking_util_with_v1_optimizers_test.py"],
    tags = [
        "notsan",  # b/74395663
    ],
    deps = [
        "//tensorflow/python:checkpoint_management",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:extra_py_tests_deps",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:resource_variable_ops",
        "//tensorflow/python:saver",
        "//tensorflow/python:state_ops",
        "//tensorflow/python:training_lib",
        "//tensorflow/python:training_util",
        "//tensorflow/python/distribute:mirrored_strategy",
        "//tensorflow/python/eager:backprop",
        "//tensorflow/python/eager:context",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:test",
        "//tensorflow/python/keras:combinations",
        "//tensorflow/python/keras/engine",
        "//tensorflow/python/keras/layers:core",
        "//tensorflow/python/training/tracking",
        "//tensorflow/python/training/tracking:graph_view",
        "//tensorflow/python/training/tracking:util",
    ],
)

tf_xla_py_test(
    name = "tracking_util_xla_test",
    srcs = ["tracking_util_xla_test.py"],
    python_version = "PY3",
    tags = [
        "no_pip",
        "no_windows",
        "nomac",
        "notsan",  # b/74395663
    ],
    deps = [
        "//tensorflow/compiler/tests:xla_test",
        "//tensorflow/python:checkpoint_management",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python/eager:backprop",
        "//tensorflow/python/keras:metrics",
        "//tensorflow/python/keras/engine",
        "//tensorflow/python/keras/layers:core",
        "//tensorflow/python/keras/optimizer_v2",
        "//tensorflow/python/training/tracking",
        "//tensorflow/python/training/tracking:util",
    ],
)

py_library(
    name = "get_config_samples",
    srcs = ["get_config_samples.py"],
    srcs_version = "PY2AND3",
    deps = [],
)
