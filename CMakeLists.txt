cmake_minimum_required(VERSION 3.2)
project(sqlparser)


set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)

add_library(${PROJECT_NAME} SHARED
    src/SQLParser.cpp
    src/SQLParserResult.cpp
    
    src/util/sqlhelper.cpp
    
    src/parser/bison_parser.cpp
    src/parser/flex_lexer.cpp

    src/sql/Expr.cpp
    src/sql/PrepareStatement.cpp
    src/sql/SQLStatement.cpp
    src/sql/statements.cpp
)
target_include_directories(${PROJECT_NAME} PUBLIC src)

if(MSVC)
    target_compile_definitions(${PROJECT_NAME} PRIVATE
	YY_NO_UNISTD_H
	strncasecmp=_strnicmp
	strcasecmp=_stricmp
	)
endif()

add_executable(example example/example.cpp)
target_link_libraries(example ${PROJECT_NAME})

