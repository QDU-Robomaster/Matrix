# CMakeLists.txt for Matrix

# Add module to include path
target_include_directories(xr PUBLIC ${CMAKE_CURRENT_LIST_DIR})

# Auto-include source files
file(GLOB MODULE_MATRIX_SRC CONFIGURE_DEPENDS
  "${CMAKE_CURRENT_LIST_DIR}/*.cpp"
  "${CMAKE_CURRENT_LIST_DIR}/*.cxx"
  "${CMAKE_CURRENT_LIST_DIR}/*.cc"
  "${CMAKE_CURRENT_LIST_DIR}/*.c"
)

target_sources(xr PRIVATE ${MODULE_MATRIX_SRC})

# ==== CMSIS-DSP: Matrix functions used by Matrixf ====
target_sources(xr PRIVATE
  ${CMAKE_SOURCE_DIR}/Drivers/CMSIS/DSP/Source/MatrixFunctions/arm_mat_init_f32.c
  ${CMAKE_SOURCE_DIR}/Drivers/CMSIS/DSP/Source/MatrixFunctions/arm_mat_add_f32.c
  ${CMAKE_SOURCE_DIR}/Drivers/CMSIS/DSP/Source/MatrixFunctions/arm_mat_sub_f32.c
  ${CMAKE_SOURCE_DIR}/Drivers/CMSIS/DSP/Source/MatrixFunctions/arm_mat_mult_f32.c
  ${CMAKE_SOURCE_DIR}/Drivers/CMSIS/DSP/Source/MatrixFunctions/arm_mat_scale_f32.c
  ${CMAKE_SOURCE_DIR}/Drivers/CMSIS/DSP/Source/MatrixFunctions/arm_mat_trans_f32.c
)

target_include_directories(xr PUBLIC
  ${CMAKE_SOURCE_DIR}/Drivers/CMSIS/DSP/Include
  ${CMAKE_SOURCE_DIR}/Drivers/CMSIS/Include
)

target_compile_definitions(xr PUBLIC
  ARM_MATH_CM4
)

# INTERFACE deps shell
get_filename_component(_MODULE_DIRNAME ${CMAKE_CURRENT_LIST_DIR} NAME)
set(_DEPS_TARGET "${_MODULE_DIRNAME}_deps")
add_library(${_DEPS_TARGET} INTERFACE)


# Register to global
set_property(GLOBAL APPEND PROPERTY XR_MODULE_DEPS ${_DEPS_TARGET})
