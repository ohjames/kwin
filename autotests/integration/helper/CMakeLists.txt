add_executable(copy copy.cpp)
target_link_libraries(copy Qt5::Gui)
ecm_mark_as_test(copy)
######################
add_executable(paste paste.cpp)
target_link_libraries(paste Qt5::Gui)
ecm_mark_as_test(paste)
