set(INCLUDES "${SENSORY_SOURCE_DIR}/include" "${SENSORY_SOURCE_DIR}/../acsdkKWDImplementations/include" "${SENSORY_KEY_WORD_DETECTOR_INCLUDE_DIR}")

set(INPUTFOLDER "${SENSORY_SOURCE_DIR}/../acsdkKWDImplementations/inputs")

discover_unit_tests("${INCLUDES}" SENSORY "${INPUTFOLDER}")