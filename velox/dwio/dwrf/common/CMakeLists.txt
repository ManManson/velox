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

add_library(
  velox_dwio_dwrf_common
  ByteRLE.cpp
  Common.cpp
  Compression.cpp
  Config.cpp
  DataBufferHolder.cpp
  Decryption.cpp
  Encryption.cpp
  EncryptionSpecification.cpp
  FileMetadata.cpp
  IntEncoder.cpp
  OutputStream.cpp
  PagedInputStream.cpp
  PagedOutputStream.cpp
  RLEv1.cpp
  RLEv2.cpp
  Statistics.cpp
  wrap/dwrf-proto-wrapper.cpp
  wrap/orc-proto-wrapper.cpp)

add_dependencies(velox_dwio_dwrf_common velox_dwio_dwrf_proto)

target_link_libraries(
  velox_dwio_dwrf_common velox_common_base velox_dwio_common
  velox_dwio_common_compression velox_dwio_dwrf_proto velox_caching)

install(TARGETS velox_dwio_dwrf_common OPTIONAL)
set(velox_dwio_dwrf_common_headers
    ByteRLE.h
    Checksum.h
    Common.h
    Compression.h
    CompressionBufferPool.h
    Config.h
    DataBufferHolder.h
    DecoderUtil.h
    Decryption.h
    EncoderUtil.h
    Encryption.h
    EncryptionCommon.h
    EncryptionSpecification.h
    FileMetadata.h
    FloatingPointDecoder.h
    IntEncoder.h
    NextVisitor.h
    OutputStream.h
    PagedInputStream.h
    PagedOutputStream.h
    RLEv1.h
    RLEv2.h
    Statistics.h)
install(FILES ${velox_dwio_dwrf_common_headers} DESTINATION "include/velox/dwio/dwrf/common")
install(FILES "wrap/coded-stream-wrapper.h"
              "wrap/dwrf-proto-wrapper.h"
              "wrap/orc-proto-wrapper.h" DESTINATION "include/velox/dwio/dwrf/common/wrap")
