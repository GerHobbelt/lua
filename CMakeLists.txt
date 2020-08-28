cmake_minimum_required(VERSION 3.7)
project(lua VERSION 5.4.0)

add_library(lua_obj OBJECT lapi.c lcode.c lctype.c ldebug.c ldo.c ldump.c
lfunc.c lgc.c llex.c lmem.c lobject.c lopcodes.c lparser.c lstate.c lstring.c
ltable.c ltm.c lundump.c lvm.c lzio.c ltests.c lauxlib.c lbaselib.c ldblib.c
liolib.c lmathlib.c loslib.c ltablib.c lstrlib.c lutf8lib.c loadlib.c
lcorolib.c linit.c)
target_include_directories(lua_obj INTERFACE ${CMAKE_CURRENT_SOURCE_DIR})

add_library(lua_static STATIC $<TARGET_OBJECTS:lua_obj>)
add_library(lua SHARED $<TARGET_OBJECTS:lua_obj>)
add_executable(lua_exe $<TARGET_OBJECTS:lua_obj> lua.c)
set_target_properties(lua_exe PROPERTIES OUTPUT_NAME lua)

install(TARGETS lua_static lua lua_exe RUNTIME DESTINATION bin ARCHIVE DESTINATION lib
LIBRARY DESTINATION lib)
file(GLOB LUA_HEADERS *.h)
install(FILES ${LUA_HEADERS} DESTINATION include)

