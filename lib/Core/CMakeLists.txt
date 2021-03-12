set( LLVM_LINK_COMPONENTS
  Object
  BinaryFormat
  )

add_tapi_library(tapiCore
  Architecture.cpp
  ArchitectureSet.cpp
  API.cpp
  APIJSONSerializer.cpp
  APIPrinter.cpp
  APIVisitor.cpp
  AvailabilityInfo.cpp
  FakeSymbols.cpp
  FileListReader.cpp
  FileManager.cpp
  FileSystem.cpp
  Framework.cpp
  HeaderFile.cpp
  InterfaceFile.cpp
  InterfaceFileManager.cpp
  MachODylibReader.cpp
  MachOReader.cpp
  PackedVersion.cpp
  Path.cpp
  Platform.cpp
  ReexportFileWriter.cpp
  Registry.cpp
  TapiError.cpp
  Target.cpp
  TextStub.cpp
  TextStubv4.cpp
  TextStubCommon.cpp
  Utils.cpp
  XPI.cpp
  XPISet.cpp
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
