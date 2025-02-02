load("@tensorflow_gnn//tensorflow_gnn:tensorflow_gnn.bzl", "pytype_strict_library")
load("@tensorflow_gnn//tensorflow_gnn:tensorflow_gnn.bzl", "tf_py_test")
load("@tensorflow_gnn//tensorflow_gnn:tensorflow_gnn.bzl", "distribute_py_test")

licenses(["notice"])

pytype_strict_library(
    name = "layers",
    srcs = ["layers.py"],
    srcs_version = "PY3",
    visibility = [
        "//tensorflow_gnn/models/contrastive_losses:__pkg__",
    ],
    deps = [
        "//:expect_tensorflow_installed",
    ],
)

tf_py_test(
    name = "layers_test",
    srcs = ["layers_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":layers",
        "//:expect_absl_installed",
        "//:expect_tensorflow_installed",
    ],
)

pytype_strict_library(
    name = "tasks",
    srcs = ["tasks.py"],
    srcs_version = "PY3",
    visibility = [
        "//tensorflow_gnn/models/contrastive_losses:__pkg__",
    ],
    deps = [
        ":layers",
        "//:expect_tensorflow_installed",
        "//tensorflow_gnn",
        "//tensorflow_gnn/models/contrastive_losses:layers",
        "//tensorflow_gnn/runner",
    ],
)

tf_py_test(
    name = "tasks_test",
    srcs = ["tasks_test.py"],
    python_version = "PY3",
    srcs_version = "PY3",
    deps = [
        ":tasks",
        "//:expect_absl_installed",
        "//:expect_tensorflow_installed",
        "//tensorflow_gnn",
    ],
)

distribute_py_test(
    name = "distribute_test",
    size = "large",
    srcs = ["distribute_test.py"],
    shard_count = 4,
    tags = [
        "no_oss",  # TODO(b/238827505)
        "nomultivm",  # TODO(b/170502145)
    ],
    xla_enable_strict_auto_jit = False,
    deps = [
        ":tasks",
        "//:expect_tensorflow_installed",
        "//tensorflow_gnn",
        "//tensorflow_gnn/models/vanilla_mpnn",
        "//tensorflow_gnn/runner",
    ],
)
