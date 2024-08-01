
include_directories(../lsinc)
include_directories(../inci)

add_definitions(-D_CRT_SECURE_NO_WARNINGS -D_NO_WINDOWS)

file(GLOB_RECURSE msls_header ../lsinc/*.h)
file(GLOB_RECURSE msls_src *.c)

source_group("Header Files" FILES ${msls_header})
source_group("Source Files" FILES ${msls_src} msls.rc)

add_library(msls31 SHARED ${msls_src} ${msls_header})
set_target_properties(msls31 PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
set_target_properties(msls31 PROPERTIES LINK_FLAGS "/DEF:msls3.def")
