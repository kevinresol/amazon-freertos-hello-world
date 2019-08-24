cmake_minimum_required(VERSION 3.13)

project(my_app)

add_executable(my_app main.c)

include_directories(my_app PRIVATE "amazon-freertos/demos/include")
include_directories(my_app PRIVATE "amazon-freertos/demos/network_manager")
include_directories(my_app PRIVATE "amazon-freertos/libraries/c_sdk/standard/ble/include")

# Tell IDF build to link against this target
set(IDF_PROJECT_EXECUTABLE my_app)

get_filename_component(EXTRA_COMPONENT_DIRS
   "components/u8g2" ABSOLUTE
)

# Add some external components to the project
set(IDF_EXTRA_COMPONENT_DIRS ${EXTRA_COMPONENT_DIRS})

# AFR_BOARD tells which board we need to target.
set(AFR_BOARD espressif.esp32_devkitc CACHE INTERNAL "")

add_subdirectory(amazon-freertos)

target_link_libraries(my_app PRIVATE AFR::wifi)
target_link_libraries(my_app PRIVATE AFR::utils)
target_link_libraries(my_app PRIVATE AFR::ble_hal)
target_link_libraries(my_app PRIVATE AFR::platform)
target_link_libraries(my_app PRIVATE AFR::dev_mode_key_provisioning)
target_link_libraries(my_app PRIVATE AFR::pkcs11)
target_link_libraries(my_app PRIVATE 3rdparty::pkcs11)
# target_link_libraries(my_app PRIVATE AFR::mqtt)