project(inject-helper)

set(inject-helper_HEADERS
	../inject-library.h
	../obfuscate.h)

set(inject-helper_SOURCES
	../inject-library.c
	../obfuscate.c
	inject-helper.c)

if(MSVC)
	add_compile_options("$<$<CONFIG:RelWithDebInfo>:/MT>")
endif()

add_executable(inject-helper
	${inject-helper_SOURCES})

target_link_libraries(inject-helper)

if(CMAKE_SIZEOF_VOID_P EQUAL 8)
	set(_output_suffix "64")
else()
	set(_output_suffix "32")
endif()

set_target_properties(inject-helper
	PROPERTIES
		OUTPUT_NAME "inject-helper${_output_suffix}")

install_obs_datatarget(inject-helper "plugins/win-capture")
