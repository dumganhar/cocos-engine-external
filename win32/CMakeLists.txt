add_library(dbgcore SHARED IMPORTED GLOBAL)

set_target_properties(dbgcore PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/dbgcore.dll
)

add_library(dbghelp SHARED IMPORTED GLOBAL)

set_target_properties(dbghelp PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/dbghelp.dll
)

add_library(dbgeng SHARED IMPORTED GLOBAL)

set_target_properties(dbgeng PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/dbgeng.dll
)

add_library(freetype STATIC IMPORTED GLOBAL)

set_target_properties(freetype PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/freetype.lib
)

add_library(glew32 SHARED IMPORTED GLOBAL)

set_target_properties(glew32 PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/glew32.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/glew32.lib
)

add_library(iconv SHARED IMPORTED GLOBAL)

set_target_properties(iconv PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/iconv.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libiconv.lib
)


add_library(crypto STATIC IMPORTED GLOBAL)

set_target_properties(crypto PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libcrypto.lib
  #IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libcrypto.lib
  #IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libcrypto-1_1.dll
)


add_library(curl SHARED IMPORTED GLOBAL)

set_target_properties(curl PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libcurl.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libcurl.lib
)

add_library(jpeg STATIC IMPORTED GLOBAL)

set_target_properties(jpeg PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libjpeg.lib
)

add_library(mpg123 SHARED IMPORTED GLOBAL)

set_target_properties(mpg123 PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libmpg123.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libmpg123.lib
)

add_library(ogg SHARED IMPORTED GLOBAL)

set_target_properties(ogg PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libogg.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libogg.lib
)

add_library(png SHARED IMPORTED GLOBAL)

set_target_properties(png PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libpng16.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libpng16.lib
)


add_library(ssl STATIC IMPORTED GLOBAL)

set_target_properties(ssl PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libssl.lib
  #IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libssl-1_1.dll
)

add_library(uv STATIC IMPORTED GLOBAL)

set_target_properties(uv PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libuv.lib
  INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include/uv
)


add_library(vorbis SHARED IMPORTED GLOBAL)

set_target_properties(vorbis PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libvorbis.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libvorbis.lib
)

add_library(vorbisfile SHARED IMPORTED GLOBAL)

set_target_properties(vorbisfile PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libvorbisfile.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libvorbisfile.lib
)

add_library(webp STATIC IMPORTED GLOBAL)

set_target_properties(webp PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libwebp.lib
)

add_library(zlib STATIC IMPORTED GLOBAL)

set_target_properties(zlib PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/libzlib.lib
  #IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/zlib1.dll
  INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include/zlib
)

add_library(websockets SHARED IMPORTED GLOBAL)

set_target_properties(websockets PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/websockets.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/websockets.lib
)


add_library(OpenAL32 SHARED IMPORTED GLOBAL)

set_target_properties(OpenAL32 PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/OpenAL32.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/OpenAL32.lib
  INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include/OpenalSoft
)

add_library(sqlite3 SHARED IMPORTED GLOBAL)

set_target_properties(sqlite3 PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/sqlite3.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/sqlite3.lib
)


add_library(SDL2 SHARED IMPORTED GLOBAL)
set_target_properties(SDL2 PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/SDL2.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/SDL2.lib
)

add_library(SDL2Main SHARED IMPORTED GLOBAL)
set_target_properties(SDL2Main PROPERTIES
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/SDL2Main.lib
)

add_library(tcmalloc SHARED IMPORTED GLOBAL)
set_target_properties(tcmalloc PROPERTIES
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/libtcmalloc_minimal.lib
)

set(se_libs_name)

if(USE_SE_V8)

    add_library(v8 SHARED IMPORTED GLOBAL)
    set_target_properties(v8 PROPERTIES
      IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/v8.dll
      IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/v8.dll.lib
    )

    add_library(v8_libbase SHARED IMPORTED GLOBAL)
    set_target_properties(v8_libbase PROPERTIES
      IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/v8_libbase.dll
      IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/v8_libbase.dll.lib
    )

    add_library(v8_libplatform SHARED IMPORTED GLOBAL)
    set_target_properties(v8_libplatform PROPERTIES
      IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/v8_libplatform.dll
      IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/v8_libplatform.dll.lib
    )

    target_link_libraries(v8 INTERFACE v8_libbase v8_libplatform)

    set_target_properties(v8 PROPERTIES
      INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include/v8
      INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_CURRENT_LIST_DIR}/include/v8
    )

    set(se_libs_name v8)
else()
   message(FATAL_ERROR "Only V8 is supported!")
endif()

############################# glslang #############################

set(glslang_libs_name glslang glslang-default-resource-limits MachineIndependent OGLCompiler OSDependent SPIRV SPIRV-Tools SPIRV-Tools-opt GenericCodeGen)
foreach(gl IN LISTS glslang_libs_name)
  add_library(${gl} STATIC IMPORTED GLOBAL)
  set_target_properties(${gl} PROPERTIES
    IMPORTED_LOCATION_DEBUG ${CMAKE_CURRENT_LIST_DIR}/libs/glslang/${gl}d.lib
    IMPORTED_LOCATION_RELEASE ${CMAKE_CURRENT_LIST_DIR}/libs/glslang/${gl}.lib
  )
endforeach()

############################# TBB #############################

add_library(tbb SHARED IMPORTED GLOBAL)
set_target_properties(tbb PROPERTIES
  IMPORTED_LOCATION ${CMAKE_CURRENT_LIST_DIR}/libs/tbb.dll
  IMPORTED_IMPLIB ${CMAKE_CURRENT_LIST_DIR}/libs/tbb.lib
)
set(tbb_libs_name tbb)

list(APPEND CC_EXTERNAL_PRIVATE_DEFINITIONS __TBB_LIB_NAME=tbb)

######################## PhysX ##############################

if(USE_PHYSICS_PHYSX)
  set(PhysXSDK PhysX PhysXCommon PhysXFoundation PhysXExtensions PhysXCooking PhysXCharacterKinematic PhysXVehicle PhysXPvdSDK)
  foreach(PX IN LISTS PhysXSDK)
    add_library(${PX} STATIC IMPORTED GLOBAL)
    set_target_properties(${PX} PROPERTIES
      IMPORTED_LOCATION_DEBUG ${CMAKE_CURRENT_LIST_DIR}/libs/PhysX/debug/${PX}_static_32.lib
      IMPORTED_LOCATION_RELEASE ${CMAKE_CURRENT_LIST_DIR}/libs/PhysX/release/${PX}_static_32.lib
    )
  endforeach()
else()
  set(PhysXSDK)
endif()

list(APPEND CC_EXTERNAL_LIBS
    freetype
    glew32
    iconv
    crypto
    curl
    jpeg
    mpg123
    ogg
    png
    ssl
    uv
    vorbis
    vorbisfile
    webp
    OpenAL32
    sqlite3
    websockets
    SDL2
    SDL2Main
    tcmalloc
    ${glslang_libs_name}
    ${tbb_libs_name}
    ${PhysXSDK}
)


set(ZLIB zlib)
if(NOT USE_MODULES)
  list(APPEND CC_EXTERNAL_LIBS ${ZLIB}
    ${se_libs_name}
  )
endif()


list(APPEND CC_EXTERNAL_INCLUDES
  ${CMAKE_CURRENT_LIST_DIR}/include
)
