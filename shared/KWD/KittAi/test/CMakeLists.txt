set(INCLUDES "${KITTAI_SOURCE_DIR}/include" "${KITTAI_SOURCE_DIR}/../acsdkKWDImplementations/include" "${KITTAI_KEY_WORD_DETECTOR_INCLUDE_DIR}")

set(INPUTFOLDER "${KITTAI_SOURCE_DIR}/../acsdkKWDImplementations/inputs")

discover_unit_tests("${INCLUDES}" KITTAI "${INPUTFOLDER}")