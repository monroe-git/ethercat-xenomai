add_executable(MAXPOS_CSP main.c servo.c ecat_dc.c)
target_include_directories(MAXPOS_CSP PUBLIC ${Xenomai_NATIVE_INCLUDE_DIRS})
target_link_libraries(MAXPOS_CSP ${Xenomai_NATIVE_DL_FLAGS} soem m)
set_target_properties(MAXPOS_CSP PROPERTIES COMPILE_FLAGS ${Xenomai_NATIVE_DEFINITIONS})
