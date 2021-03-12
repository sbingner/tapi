set( LLVM_LINK_COMPONENTS
  Object
  BinaryFormat
  )

add_tapi_library(tapiCore
  Architecture.cpp
  ArchitectureSet.cpp
  ArchitectureSupport.cpp
  API.cpp
  APIPrinter.cpp
  APIVisitor.cpp
  AvailabilityInfo.cpp
  FakeSymbols.cpp
  FileManager.cpp
  FileSystem.cpp
  Framework.cpp
  ExtendedInterfaceFile.cpp
  HeaderFile.cpp
  InterfaceFile.cpp
  InterfaceFileBase.cpp
  InterfaceFileManager.cpp
  JSONFile.cpp
  MachODylibReader.cpp
  Path.cpp
  Platform.cpp
  ReexportFileWriter.cpp
  Registry.cpp
  Symbol.cpp
  TapiError.cpp
  TextStub_v1.cpp
  TextStub_v2.cpp
  TextStub_v3.cpp
  Utils.cpp
  XPI.cpp
  XPISet.cpp
  YAML.cpp
  YAMLReaderWriter.cpp

  LINK_LIBS
  clangBasic
  )
add_dependencies(tapiCore clang-resource-headers)
if(Clang_DIR)
    set(clang_lib_dir ${Clang_DIR}/../..)
elseif(LLVM_DIR)
    set(clang_lib_dir ${LLVM_DIR}/../..)
elseif(LLVM_LIBRARY_DIRS)
    set(clang_lib_dir ${LLVM_LIBRARY_DIRS})
elseif(LLVM_BUILD_LIBRARY_DIR)
    set(clang_lib_dir ${LLVM_BUILD_LIBRARY_DIR})
elseif(LLVM_BINARY_DIR)
    set(clang_lib_dir ${LLVM_BINARY_DIR}/lib${LLVM_LIBDIR_SUFFIX})
endif()
set(clang_version ${LLVM_VERSION_MAJOR}.${LLVM_VERSION_MINOR}.${LLVM_VERSION_PATCH})
set(clang_resource_headers_dir ${clang_lib_dir}/clang/${clang_version}/include)
if(NOT EXISTS ${clang_resource_headers_dir})
    message(WARNING "Expected directory for clang-resource headers not found: ${clang_resource_headers_dir}")
endif()
