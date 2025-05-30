load("@llvm-project//mlir:tblgen.bzl", "gentbl_cc_library", "td_library")

package(
    # copybara:uncomment default_applicable_licenses = ["//tensorflow:license"],
    default_visibility = [":friends"],
    licenses = ["notice"],
)

package_group(
    name = "friends",
    includes = [
        "//xla:friends",
    ],
)

td_library(
    name = "xla_gpu_td_files",
    srcs = glob(["*.td"]),
    includes = ["."],
    deps = [
        "//xla/codegen/emitters/ir:xla_td_files",
        "@llvm-project//mlir:BuiltinDialectTdFiles",
        "@llvm-project//mlir:CallInterfacesTdFiles",
        "@llvm-project//mlir:ControlFlowInterfacesTdFiles",
        "@llvm-project//mlir:InferTypeOpInterfaceTdFiles",
        "@llvm-project//mlir:OpBaseTdFiles",
        "@llvm-project//mlir:SideEffectInterfacesTdFiles",
    ],
)

gentbl_cc_library(
    name = "xla_gpu_dialect_inc_gen",
    strip_include_prefix = ".",
    tbl_outs = [
        (
            ["-gen-dialect-decls"],
            "xla_gpu_dialect.h.inc",
        ),
        (
            ["-gen-dialect-defs"],
            "xla_gpu_dialect.cc.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "xla_gpu_dialect.td",
    deps = [":xla_gpu_td_files"],
)

gentbl_cc_library(
    name = "xla_gpu_ops_inc_gen",
    strip_include_prefix = ".",
    tbl_outs = [
        (
            ["-gen-op-decls"],
            "xla_gpu_ops.h.inc",
        ),
        (
            ["-gen-op-defs"],
            "xla_gpu_ops.cc.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "xla_gpu_ops.td",
    deps = [":xla_gpu_td_files"],
)

gentbl_cc_library(
    name = "xla_gpu_attrs_inc_gen",
    strip_include_prefix = ".",
    tbl_outs = [
        (
            ["-gen-enum-decls"],
            "xla_gpu_enums.h.inc",
        ),
        (
            ["-gen-enum-defs"],
            "xla_gpu_enums.cc.inc",
        ),
        (
            [
                "-gen-attrdef-decls",
                "-attrdefs-dialect=xla_gpu",
            ],
            "xla_gpu_attrs.h.inc",
        ),
        (
            [
                "-gen-attrdef-defs",
                "-attrdefs-dialect=xla_gpu",
            ],
            "xla_gpu_attrs.cc.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "xla_gpu_attrs.td",
    deps = [":xla_gpu_td_files"],
)

gentbl_cc_library(
    name = "xla_gpu_types_inc_gen",
    strip_include_prefix = ".",
    tbl_outs = [
        (
            [
                "-gen-typedef-decls",
                "-typedefs-dialect=xla_gpu",
            ],
            "xla_gpu_types.h.inc",
        ),
        (
            [
                "-gen-typedef-defs",
                "-typedefs-dialect=xla_gpu",
            ],
            "xla_gpu_types.cc.inc",
        ),
    ],
    tblgen = "@llvm-project//mlir:mlir-tblgen",
    td_file = "xla_gpu_types.td",
    deps = [":xla_gpu_td_files"],
)

cc_library(
    name = "xla_gpu",
    srcs = [
        "xla_gpu_attrs.cc",
        "xla_gpu_dialect.cc",
        "xla_gpu_ops.cc",
        "xla_gpu_types.cc",
    ],
    hdrs = ["xla_gpu_ops.h"],
    deps = [
        ":xla_gpu_attrs_inc_gen",
        ":xla_gpu_dialect_inc_gen",
        ":xla_gpu_ops_inc_gen",
        ":xla_gpu_types_inc_gen",
        "//xla/codegen/emitters/ir:xla",
        "//xla/hlo/analysis:indexing_analysis",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/status:statusor",
        "@com_google_absl//absl/strings",
        "@llvm-project//llvm:Support",
        "@llvm-project//mlir:ArithDialect",
        "@llvm-project//mlir:BytecodeOpInterface",
        "@llvm-project//mlir:CallOpInterfaces",
        "@llvm-project//mlir:FuncDialect",
        "@llvm-project//mlir:IR",
        "@llvm-project//mlir:InferTypeOpInterface",
        "@llvm-project//mlir:InliningUtils",
        "@llvm-project//mlir:SideEffectInterfaces",
        "@llvm-project//mlir:Support",
    ],
)
