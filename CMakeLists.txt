# To use this example as a standalone project using CMake:
# mkdir build
# cd build
# cmake .. -DCMAKE_TOOLCHAIN_FILE=path/to/Retro68-build/toolchain/m68k-apple-macos/cmake/retro68.toolchain.cmake
# make

cmake_minimum_required(VERSION 2.8)

add_application(PetProject
	constants.h
	main.c
	MainApp.c
	dialog.r
	menus.r
	pika.r
	)

# Enable -ffunction-sections and -gc-sections to make the app as small as possible
# On 68K, also enable --mac-single to build it as a single-segment app (so that this code path doesn't rot)
set_target_properties(PetProject PROPERTIES COMPILE_OPTIONS -ffunction-sections)
if(CMAKE_SYSTEM_NAME MATCHES Retro68)
	set_target_properties(PetProject PROPERTIES LINK_FLAGS "-Wl,-gc-sections -Wl,--mac-single")

else()
	set_target_properties(PetProject PROPERTIES LINK_FLAGS "-Wl,-gc-sections")
endif()
