aux_source_directory(. rime_api_src)
aux_source_directory(rime rime_base_src)
aux_source_directory(rime/algo rime_algo_src)
aux_source_directory(rime/config rime_config_src)
aux_source_directory(rime/dict rime_dict_src)
aux_source_directory(rime/gear rime_gears_src)
aux_source_directory(rime/lever rime_levers_src)

if(rime_plugins_library)
  aux_source_directory(../plugins rime_plugins_src)
endif()

set(rime_src
    ${rime_api_src} ${rime_base_src} ${rime_config_src} #core
    ${rime_algo_src} ${rime_dict_src} #dict
    ${rime_gears_src}
    ${rime_levers_src}
    ${rime_plugins_src}
    ${rime_plugins_objs})

set(rime_optional_deps "")
if(ENABLE_EXTERNAL_PLUGINS)
  set(rime_optional_deps ${rime_optional_deps} dl)
endif()

set(rime_dependencies
    yaml-cpp ${CMAKE_THREAD_LIBS_INIT} ${rime_optional_deps} #core
    leveldb marisa #dict
    opencc ${ICONV_LIBRARIES} ${ICU_LIBRARIES} #gear
    ${rime_plugins_deps})

if(BUILD_SHARED_LIBS)
  add_library(rime ${rime_src})
  target_link_libraries(rime ${rime_dependencies})
  set_target_properties(rime PROPERTIES
    DEFINE_SYMBOL "RIME_EXPORTS"
    VERSION ${rime_version}
    SOVERSION ${rime_soversion}
    LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib
    RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)
  install(TARGETS rime DESTINATION ${CMAKE_INSTALL_FULL_LIBDIR})
else()
  add_library(rime-static STATIC ${rime_src})
  target_link_libraries(rime-static ${rime_dependencies})
  set_target_properties(rime-static PROPERTIES
    OUTPUT_NAME "rime" PREFIX "lib"
    ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
  install(TARGETS rime-static DESTINATION ${CMAKE_INSTALL_FULL_LIBDIR})
endif()
