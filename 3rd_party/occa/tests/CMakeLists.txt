# Test occa binary (based on run_bin_tests)
if (ENABLE_UTILITY)
  add_test(NAME occa-autocomplete            COMMAND occa autocomplete)
  add_test(NAME occa-clear                   COMMAND occa clear)
  add_test(NAME occa-compile-help            COMMAND occa compile --help)
  add_test(NAME occa-env                     COMMAND occa env)
  add_test(NAME occa-info                    COMMAND occa info)
  add_test(NAME occa-modes                   COMMAND occa modes)
  add_test(NAME occa-translate-help          COMMAND occa translate --help)
  add_test(NAME occa-translate-serial        COMMAND occa translate --mode Serial ${OCCA_SOURCE_DIR}/examples/cpp/01_add_vectors/addVectors.okl)
  if (OCCA_OPENMP_ENABLED)
    add_test(NAME occa-translate-openmp          COMMAND occa translate --mode OpenMP ${OCCA_SOURCE_DIR}/examples/cpp/01_add_vectors/addVectors.okl)
    set_property(TEST occa-translate-openmp APPEND PROPERTY ENVIRONMENT OCCA_CACHE_DIR=${OCCA_BUILD_DIR}/occa)
  endif()
  if (OCCA_CUDA_ENABLED)
    add_test(NAME occa-translate-cuda          COMMAND occa translate --mode CUDA ${OCCA_SOURCE_DIR}/examples/cpp/01_add_vectors/addVectors.okl)
    add_test(NAME occa-translate-cuda-launcher COMMAND occa translate --mode CUDA --launcher ${OCCA_SOURCE_DIR}/examples/cpp/01_add_vectors/addVectors.okl)
    set_property(TEST occa-translate-cuda occa-translate-cuda-launcher APPEND PROPERTY ENVIRONMENT OCCA_CACHE_DIR=${OCCA_BUILD_DIR}/occa)
  endif()
  if (OCCA_HIP_ENABLED)
    add_test(NAME occa-translate-hip          COMMAND occa translate --mode HIP ${OCCA_SOURCE_DIR}/examples/cpp/01_add_vectors/addVectors.okl)
    add_test(NAME occa-translate-hip-launcher COMMAND occa translate --mode HIP --launcher ${OCCA_SOURCE_DIR}/examples/cpp/01_add_vectors/addVectors.okl)
    set_property(TEST occa-translate-hip occa-translate-hip-launcher APPEND PROPERTY ENVIRONMENT OCCA_CACHE_DIR=${OCCA_BUILD_DIR}/occa)
  endif()
  if (OCCA_OPENCL_ENABLED)
    add_test(NAME occa-translate-opencl          COMMAND occa translate --mode OpenCL ${OCCA_SOURCE_DIR}/examples/cpp/01_add_vectors/addVectors.okl)
    add_test(NAME occa-translate-opencl-launcher COMMAND occa translate --mode OpenCL --launcher ${OCCA_SOURCE_DIR}/examples/cpp/01_add_vectors/addVectors.okl)
    set_property(TEST occa-translate-opencl occa-translate-opencl-launcher APPEND PROPERTY ENVIRONMENT OCCA_CACHE_DIR=${OCCA_BUILD_DIR}/occa)
  endif()
  add_test(NAME occa-version                 COMMAND occa version)

  set_property(TEST occa-autocomplete occa-clear occa-compile-help occa-env occa-info occa-modes occa-translate-help occa-translate-serial occa-version APPEND PROPERTY ENVIRONMENT OCCA_CACHE_DIR=${OCCA_BUILD_DIR}/occa)
endif (ENABLE_UTILITY)

add_subdirectory(src)
