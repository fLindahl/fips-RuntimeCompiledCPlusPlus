#
# project: fips-RuntimeCompiledCPlusPlus
#
cmake_minimum_required(VERSION 2.8)

# include the fips main cmake file
get_filename_component(FIPS_ROOT_DIR "../fips" ABSOLUTE)
include("${FIPS_ROOT_DIR}/cmake/fips.cmake")

fips_setup()
fips_project(fips-RuntimeCompiledCPlusPlus)
set(BUILD_EXAMPLES off)

# Runtime Compiler
fips_begin_lib(RuntimeCompiler)

fips_ide_group(Imports/rccpp)
fips_include_directories(RuntimeCompiledCPlusPlus/Aurora/RuntimeCompiler)

if(UNIX)
    if(APPLE)
        fips_src(RuntimeCompiledCPlusPlus/Aurora/RuntimeCompiler EXCEPT *Windows.cpp *Win32.cpp *Linux.cpp NO_RECURSE)
    else()
        fips_src(RuntimeCompiledCPlusPlus/Aurora/RuntimeCompiler EXCEPT *Windows.cpp *Win32.cpp *OSX.cpp NO_RECURSE)
    endif()
else()
    fips_src(RuntimeCompiledCPlusPlus/Aurora/RuntimeCompiler EXCEPT *Posix.cpp *OSX.cpp *Linux.cpp  NO_RECURSE)
endif()

fips_end_lib()

# Runtime Object System
fips_begin_lib(RuntimeObjectSystem)

fips_ide_group(Imports/rccpp)
fips_include_directories(RuntimeCompiledCPlusPlus/Aurora/RuntimeObjectSystem)

if(UNIX)
    fips_src(RuntimeCompiledCPlusPlus/Aurora/RuntimeObjectSystem EXCEPT *Windows.cpp NO_RECURSE)
else()
    fips_src(RuntimeCompiledCPlusPlus/Aurora/RuntimeObjectSystem EXCEPT *Posix.cpp NO_RECURSE)
endif()

fips_end_lib()
fips_finish()


