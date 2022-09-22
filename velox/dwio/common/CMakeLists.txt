# Copyright (c) Facebook, Inc. and its affiliates.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
add_subdirectory(compression)
add_subdirectory(encryption)
add_subdirectory(exception)

if(${VELOX_BUILD_TESTING})
  add_subdirectory(tests)
elseif(${VELOX_BUILD_TEST_UTILS})
  add_subdirectory(tests/utils)
endif()

add_library(
  velox_dwio_common
  BitConcatenation.cpp
  BufferedInput.cpp
  CachedBufferedInput.cpp
  CacheInputStream.cpp
  ColumnSelector.cpp
  Common.cpp
  DataBuffer.cpp
  DataSink.cpp
  DecoderUtil.cpp
  DirectDecoder.cpp
  DwioMetricsLog.cpp
  InputStream.cpp
  IntDecoder.cpp
  IoStatistics.cpp
  MemoryInputStream.cpp
  Options.cpp
  ReaderFactory.cpp
  ScanSpec.cpp
  ColumnLoader.cpp
  SelectiveColumnReader.cpp
  SelectiveStructColumnReader.cpp
  SeekableInputStream.cpp
  TypeWithId.cpp)

target_link_libraries(
  velox_dwio_common
  velox_buffer
  velox_caching
  velox_dwio_common_compression
  velox_dwio_common_encryption
  velox_dwio_common_exception
  velox_exception
  velox_memory
  Boost::regex
  ${FOLLY_WITH_DEPENDENCIES}
  glog::glog)

install(TARGETS velox_dwio_common OPTIONAL)
set(velox_dwio_common_headers
    Adaptor.h
    BitConcatenation.h
    BufferUtil.h
    BufferedInput.h
    CacheInputStream.h
    CachedBufferedInput.h
    ChainedBuffer.h
    Closeable.h
    ColumnLoader.h
    ColumnSelector.h
    ColumnVisitors.h
    Common.h
    DataBuffer.h
    DataSink.h
    DecoderUtil.h
    DirectDecoder.h
    ErrorTolerance.h
    FilterNode.h
    FlushPolicy.h
    FormatData.h
    InputStream.h
    IntCodecCommon.h
    IntDecoder.h
    IoStatistics.h
    MemoryInputStream.h
    MetricsLog.h
    Options.h
    RandGen.h
    Reader.h
    ReaderFactory.h
    Retry.h
    ScanSpec.h
    SeekableInputStream.h
    SelectiveColumnReader.h
    SelectiveColumnReaderInternal.h
    SelectiveFloatingPointColumnReader.h
    SelectiveIntegerColumnReader.h
    SelectiveStructColumnReader.h
    Statistics.h
    StreamIdentifier.h
    StreamUtil.h
    TypeUtil.h
    TypeUtils.h
    TypeWithId.h
    )
install(FILES ${velox_dwio_common_headers} DESTINATION "include/velox/dwio/common")
install(FILES "wrap/zero-copy-stream-wrapper.h" DESTINATION "include/velox/dwio/common/wrap") 
