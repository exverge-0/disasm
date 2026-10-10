cmake_minimum_required(VERSION 3.11)

project(disasm_proxy)

include_directories("../keystone/include")
include_directories("../capstone/include")
link_directories("../keystone/llvm/lib")
link_directories("../capstone")

add_executable(disasm_proxy main.c)

set_target_properties(disasm_proxy PROPERTIES LINKER_LANGUAGE CXX)
target_link_libraries(disasm_proxy keystone capstone)

target_link_options(disasm_proxy PRIVATE -sEXPORTED_FUNCTIONS=['_malloc','_free','_ks_open','_ks_asm','_ks_free','_ks_close','_ks_errno','_ks_strerror','_cs_open','_cs_disasm','_cs_free','_cs_close','_cs_errno','_cs_strerror','_insn_mnemonic','_insn_op_str','_insn_size','_insn_struct_size'])
target_link_options(disasm_proxy PRIVATE -sEXPORTED_RUNTIME_METHODS=['intArrayFromString','intArrayToString','getValue','setValue','stringToUTF8','UTF8ToString','HEAPU8','HEAPU16','HEAP32'])
target_link_options(disasm_proxy PRIVATE -sMODULARIZE -sASSERTIONS=1)
target_link_options(disasm_proxy PRIVATE -sWASM_BIGINT=0)
