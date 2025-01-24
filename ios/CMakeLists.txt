
add_library(crypto STATIC IMPORTED GLOBAL)
set_target_properties(crypto PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libcrypto.a
)

add_library(freetype STATIC IMPORTED GLOBAL)
set_target_properties(freetype PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libfreetype.a
)

add_library(jpeg STATIC IMPORTED GLOBAL)
set_target_properties(jpeg PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libjpeg.a
)

add_library(png STATIC IMPORTED GLOBAL)
set_target_properties(png PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libpng.a
)

add_library(ssl STATIC IMPORTED GLOBAL)
set_target_properties(ssl PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libssl.a
)

add_library(uv STATIC IMPORTED GLOBAL)
set_target_properties(uv PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libuv_a.a
  INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include/uv
)

add_library(webp STATIC IMPORTED GLOBAL)
set_target_properties(webp PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libwebp.a
)

add_library(v8_monolith STATIC IMPORTED GLOBAL)
set(V8_COMPILE_FLAGS
  V8_TARGET_ARCH_ARM64
  V8_HAVE_TARGET_OS
  V8_TARGET_OS_IOS
  V8_TYPED_ARRAY_MAX_SIZE_IN_HEAP=64
  ENABLE_MINOR_MC
  V8_CONCURRENT_MARKING
  V8_ENABLE_LAZY_SOURCE_POSITIONS
  V8_EMBEDDED_BUILTINS
  V8_SHARED_RO_HEAP
  V8_WIN64_UNWINDING_INFO
  V8_ENABLE_REGEXP_INTERPRETER_THREADED_DISPATCH
  V8_31BIT_SMIS_ON_64BIT_ARCH
  V8_DEPRECATION_WARNINGS
  V8_IMMINENT_DEPRECATION_WARNINGS
  DISABLE_UNTRUSTED_CODE_MITIGATIONS
)
set_target_properties(v8_monolith PROPERTIES
    IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libv8_monolith.a
    INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include/v8
    # INTERFACE_COMPILE_DEFINITIONS ${V8_COMPILE_FLAGS}
)
set_property(TARGET v8_monolith APPEND PROPERTY INTERFACE_COMPILE_DEFINITIONS ${V8_COMPILE_FLAGS})


# add_library(inspector STATIC IMPORTED GLOBAL)
# set_target_properties(inspector PROPERTIES
#     IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libinspector.a
# )

add_library(js_static STATIC IMPORTED GLOBAL)
set_target_properties(js_static PROPERTIES
    IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libjs_static.a
    INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include/spidermonkey
)

add_library(mozglue STATIC IMPORTED GLOBAL)
set_target_properties(mozglue PROPERTIES
    IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libmozglue.a
)

set(se_libs_name)

if(USE_SE_V8)
    list(APPEND se_libs_name
        v8_monolith
        uv
        )
#    if(USE_V8_DEBUGGER)
#        list(APPEND se_libs_name)
#    endif()
endif()

if(USE_SE_JSC)
    find_library(JAVASCRIPT_CORE_LIBRARY JavaScriptCore REQUIRED)
    set(se_libs_name ${JAVASCRIPT_CORE_LIBRARY})
endif()

############################# glslang #############################

set(glslang_libs_name glslang glslang-default-resource-limits MachineIndependent OGLCompiler OSDependent SPIRV SPIRV-Tools SPIRV-Tools-opt GenericCodeGen)
foreach(gl IN LISTS glslang_libs_name)
  add_library(${gl} STATIC IMPORTED GLOBAL)
  set_target_properties(${gl} PROPERTIES
    IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/glslang/lib${gl}.a
  )
endforeach()

############################# SPIRV-Cross #############################

add_library(spirv-cross-core STATIC IMPORTED GLOBAL)
set_target_properties(spirv-cross-core PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/spirv-cross/libspirv-cross-core.a
)
add_library(spirv-cross-msl STATIC IMPORTED GLOBAL)
set_target_properties(spirv-cross-msl PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/spirv-cross/libspirv-cross-msl.a
)
add_library(spirv-cross-glsl STATIC IMPORTED GLOBAL)
set_target_properties(spirv-cross-glsl PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/spirv-cross/libspirv-cross-glsl.a
)
set(spirv-cross_libs_name spirv-cross-core spirv-cross-glsl spirv-cross-msl)

############################# TBB #############################

add_library(tbb STATIC IMPORTED GLOBAL)
set_target_properties(tbb PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libtbb_static.a
)
set(tbb_libs_name tbb)

if(USE_PHYSICS_PHYSX)
  set(PhysXSDK PhysX PhysXCommon PhysXFoundation PhysXExtensions PhysXCooking PhysXCharacterKinematic PhysXVehicle PhysXPvdSDK)
  foreach(PX IN LISTS PhysXSDK)
    add_library(${PX} STATIC IMPORTED GLOBAL)
    set_target_properties(${PX} PROPERTIES
      IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/PhysX/lib${PX}_static_64.a
    )
  endforeach()
else()
  set(PhysXSDK)
endif()

list(APPEND CC_EXTERNAL_INCLUDES
    ${CMAKE_CURRENT_LIST_DIR}/include
)

list(APPEND CC_EXTERNAL_LIBS
    freetype
    jpeg
    png
    webp
    crypto
    ssl
    ${glslang_libs_name}
    ${spirv-cross_libs_name}
    ${tbb_libs_name}
    ${PhysXSDK}
)

set(ZLIB z)
if(NOT USE_MODULES)
  list(APPEND CC_EXTERNAL_LIBS ${se_libs_name})
endif()
