add_library(cyanide STATIC)
add_library(cyanide::cyanide ALIAS cyanide)

set_property(TARGET ${PROJECT_NAME}
				PROPERTY 
					MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>"
)
target_compile_features(cyanide PUBLIC cxx_std_23)
target_include_directories(cyanide PUBLIC
	$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
	$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)

if(CYANIDE_FEATURE_HOOK)
	find_package(PolyHook_2 CONFIG REQUIRED)
	find_package(xbyak CONFIG REQUIRED)
	target_link_libraries(cyanide PUBLIC xbyak::xbyak PolyHook_2::PolyHook_2)
endif()

target_sources(cyanide PRIVATE
	"main.cpp"
	"memory_protection.cpp"
)
