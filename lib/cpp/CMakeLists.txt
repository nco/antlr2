cmake_minimum_required(VERSION 2.6)
project (antlr)

#//////////////////////////
#compile as C++/static CRT on Visual Studio 
#//////////////////////////

set(MSVC_USE_STATIC_CRT off CACHE BOOL "Use MT flags when compiling in MSVC")
if (MSVC)
  if (MSVC_USE_STATIC_CRT)
     message("-- Using static CRT ${MSVC_USE_STATIC_CRT}")
     foreach(flag_var CMAKE_CXX_FLAGS_DEBUG 
     CMAKE_CXX_FLAGS_RELEASE
     CMAKE_CXX_FLAGS_MINSIZEREL 
     CMAKE_CXX_FLAGS_RELWITHDEBINFO
     CMAKE_C_FLAGS_DEBUG 
     CMAKE_C_FLAGS_RELEASE
     CMAKE_C_FLAGS_MINSIZEREL 
     CMAKE_C_FLAGS_RELWITHDEBINFO)
     string(REPLACE "/MD" "/MT" ${flag_var} "${${flag_var}}")
     endforeach()
  endif(MSVC_USE_STATIC_CRT)
endif(MSVC)

#//////////////////////////
# compiler/linker warnings
#//////////////////////////

if(MSVC)
add_definitions(-D_CRT_SECURE_NO_WARNINGS)
add_definitions(-D_CRT_NONSTDC_NO_DEPRECATE)
set(MSVC_DEVELOPER ON CACHE BOOL "Disable MSVC warnings /wd4267 /wd4244 /wd4477")
if (MSVC_DEVELOPER)
  set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /wd4267 /wd4244 /wd4477")
  set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /wd4267 /wd4244 /wd4477")
endif(MSVC_DEVELOPER)
endif(MSVC)

set(ANTLR_SRC
    src/ANTLRUtil.cpp
    src/ASTFactory.cpp
    src/ASTNULLType.cpp
    src/ASTRefCount.cpp
    src/BaseAST.cpp
    src/BitSet.cpp
    src/CharBuffer.cpp
    src/CharScanner.cpp
    src/CommonAST.cpp
    src/CommonASTWithHiddenTokens.cpp
    src/CommonHiddenStreamToken.cpp
    src/CommonToken.cpp
    src/InputBuffer.cpp
    src/LLkParser.cpp
    src/MismatchedCharException.cpp
    src/MismatchedTokenException.cpp
    src/NoViableAltException.cpp
    src/NoViableAltForCharException.cpp
    src/Parser.cpp
    src/RecognitionException.cpp
    src/String.cpp
    src/Token.cpp
    src/TokenBuffer.cpp
    src/TokenRefCount.cpp
    src/TokenStreamBasicFilter.cpp
    src/TokenStreamHiddenTokenFilter.cpp
    src/TokenStreamRewriteEngine.cpp
    src/TokenStreamSelector.cpp
    src/TreeParser.cpp
    )

set(ANTLR_HDR
    antlr/ANTLRException.hpp
    antlr/ANTLRUtil.hpp
    antlr/AST.hpp
    antlr/ASTArray.hpp
    antlr/ASTFactory.hpp
    antlr/ASTNULLType.hpp
    antlr/ASTPair.hpp
    antlr/ASTRefCount.hpp
    antlr/BaseAST.hpp
    antlr/BitSet.hpp
    antlr/CharBuffer.hpp
    antlr/CharInputBuffer.hpp
    antlr/CharScanner.hpp
    antlr/CharStreamException.hpp
    antlr/CharStreamIOException.hpp
    antlr/CircularQueue.hpp
    antlr/CommonAST.hpp
    antlr/CommonASTWithHiddenTokens.hpp
    antlr/CommonHiddenStreamToken.hpp
    antlr/CommonToken.hpp
    antlr/IOException.hpp
    antlr/InputBuffer.hpp
    antlr/LLkParser.hpp
    antlr/LexerSharedInputState.hpp
    antlr/MismatchedCharException.hpp
    antlr/MismatchedTokenException.hpp
    antlr/NoViableAltException.hpp
    antlr/NoViableAltForCharException.hpp
    antlr/Parser.hpp
    antlr/ParserSharedInputState.hpp
    antlr/RecognitionException.hpp
    antlr/RefCount.hpp
    antlr/SemanticException.hpp
    antlr/String.hpp
    antlr/Token.hpp
    antlr/TokenBuffer.hpp
    antlr/TokenRefCount.hpp
    antlr/TokenStream.hpp
    antlr/TokenStreamBasicFilter.hpp
    antlr/TokenStreamException.hpp
    antlr/TokenStreamHiddenTokenFilter.hpp
    antlr/TokenStreamIOException.hpp
    antlr/TokenStreamRecognitionException.hpp
    antlr/TokenStreamRetryException.hpp
    antlr/TokenStreamRewriteEngine.hpp
    antlr/TokenStreamSelector.hpp
    antlr/TokenWithIndex.hpp
    antlr/TreeParser.hpp
    antlr/TreeParserSharedInputState.hpp
    antlr/config.hpp
    )

include_directories(.)

add_library(antlr ${ANTLR_SRC} ${ANTLR_HDR})

