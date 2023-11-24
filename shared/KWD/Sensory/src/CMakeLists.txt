add_definitions("-DACSDK_LOG_MODULE=sensoryKeywordDetector")
add_library(SENSORY SHARED
    SensoryKeywordDetector.cpp)

target_include_directories(SENSORY PUBLIC
	"${SENSORY_KEY_WORD_DETECTOR_INCLUDE_DIR}"
	"${SENSORY_SOURCE_DIR}/../acsdkKWDImplementations/include" 
	"${SENSORY_SOURCE_DIR}/include")

target_link_libraries(SENSORY 
    acsdkKWDInterfaces
    acsdkKWDImplementations
    acsdkManufactory
    AVSCommon 
    "${SENSORY_KEY_WORD_DETECTOR_LIB_PATH}")

# install target
asdk_install()