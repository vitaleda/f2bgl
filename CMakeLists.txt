cmake_minimum_required(VERSION 2.8)

# VitaSDK defines
if( NOT DEFINED CMAKE_TOOLCHAIN_FILE )
  if( DEFINED ENV{VITASDK} )
    set(CMAKE_TOOLCHAIN_FILE "$ENV{VITASDK}/share/vita.toolchain.cmake" CACHE PATH "toolchain file")
  else()
    message(FATAL_ERROR "Please define VITASDK to point to your SDK path!")
  endif()
endif()

# Project start
set(VITA_APPNAME FadeToBlack)
set(VITA_TITLEID "F2BGLVITA")

project(${VITA_APPNAME})
include("${VITASDK}/share/vita.cmake" REQUIRED)

# Flags and includes
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DUSE_GLES -DVITA -fno-exceptions")

include_directories(
  ${VITASDK}/arm-vita-eabi/include/SDL2
)

link_directories(
  ${CMAKE_CURRENT_BINARY_DIR}
)

# Builds
add_executable(${VITA_APPNAME}
  cabinet.cpp
  camera.cpp
  collision.cpp
  cutscene.cpp
  decoder.cpp
  file.cpp
  font.cpp
  game.cpp
  icons.cpp
  input.cpp
  installer.cpp
  inventory.cpp
  main.cpp
  menu.cpp
  mixer.cpp
  opcodes.cpp
  raycast.cpp
  render.cpp
  resource.cpp
  saveload.cpp
  scaler.cpp
  screenshot.cpp
  sound.cpp
  spritecache.cpp
  stub.cpp
  texturecache.cpp
  trigo.cpp
  util.cpp
  xmiplayer.cpp
)

target_link_libraries(${VITA_APPNAME}
  SDL2
  vita2d
  vitaGL
  WildMidi
  z
  SceAppUtil_stub
  SceAudio_stub
  SceCommonDialog_stub
  SceCtrl_stub
  SceDisplay_stub
  SceGxm_stub
  SceHid_stub
  ScePower_stub
  SceSysmodule_stub
  SceTouch_stub
)

# Create Vita artifacts
vita_create_self(eboot.bin ${VITA_APPNAME} UNSAFE)
vita_create_vpk(${VITA_APPNAME}.vpk ${VITA_TITLEID} eboot.bin
  NAME ${VITA_APPNAME}
  #FILE res/icon0.png sce_sys/icon0.png
  #FILE res/bg.png sce_sys/livearea/contents/bg.png
  #FILE res/startup.png sce_sys/livearea/contents/startup.png
  #FILE res/template.xml sce_sys/livearea/contents/template.xml
)
