include_directories(AFTER ${AMI_INCLUDE_DIRS})

enable_testing()

configure_file("amitest.sh.cmake" "amitest.sh")

set(AMITEST "${ami-project_BINARY_DIR}/tests/amitest.sh")

add_test(Functions ${AMITEST} functions.ami)
add_test(Max ${AMITEST} test-max.ami)
add_test(FieldAssignment ${AMITEST} field-assignment.ami)
add_test(Loop2ThenAction ${AMITEST} loop2-then-action.ami)
add_test(Variables ${AMITEST} vars.ami)
add_test(VariablesNonExisting ${AMITEST} non-existingvar.ami)
add_test(MixedVariables ${AMITEST} mixedvars.ami)
add_test(Strings ${AMITEST} strings.ami)
add_test(Include ${AMITEST} include.ami)
  
add_executable(aminewclose ami-new-close.c)
target_link_libraries(aminewclose ${AMI_LIBRARY} ${CMAKE_DL_LIBS})
add_test(AmiNewClose aminewclose)

add_executable(amiitems ami-items.c)
target_link_libraries(amiitems ${AMI_LIBRARY} ${CMAKE_DL_LIBS})
add_test(AmiItems amiitems)

add_executable(actionnewclose action-new-close.c)
target_link_libraries(actionnewclose ${AMI_LIBRARY} ${CMAKE_DL_LIBS})
add_test(ActionNewClose actionnewclose)

add_executable(apivars api-variables.c)
target_link_libraries(apivars ${AMI_LIBRARY} ${CMAKE_DL_LIBS})
add_test(API_Variables apivars)
