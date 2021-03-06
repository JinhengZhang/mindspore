file(GLOB_RECURSE _CURRENT_SRC_FILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "*.cc")
set_property(SOURCE ${_CURRENT_SRC_FILES} PROPERTY COMPILE_DEFINITIONS SUBMODULE_ID=mindspore::SubModuleId::SM_MD)

set(DATASET_ENGINE_OPT_SRC_FILES
    pass.cc
    post/auto_worker_pass.cc
    pre/cache_validation_pass.cc
    pre/deep_copy_pass.cc
    pre/getter_pass.cc
    pre/input_validation_pass.cc
    pre/epoch_ctrl_pass.cc
    pre/node_removal_pass.cc
    )

# This set of files is for ExecTree's optimizer. It is being migrated to IR's optimizer.
# When the migration is complete, we will remove these files.
set(DATASET_ENGINE_OPT_SRC_FILES
    ${DATASET_ENGINE_OPT_SRC_FILES}
    optional/tensor_op_fusion_pass.cc
    pre/cache_error_pass.cc
    post/repeat_pass.cc
    pre/cache_transform_pass.cc
    pre/epoch_injection_pass.cc
    util/printer_pass.cc
    pre/removal_pass.cc
    )

if (ENABLE_PYTHON)
    set(DATASET_ENGINE_OPT_SRC_FILES
        ${DATASET_ENGINE_OPT_SRC_FILES}
        post/generator_node_pass.cc
        )
endif()

add_library(engine-opt OBJECT ${DATASET_ENGINE_OPT_SRC_FILES})
