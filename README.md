# Numerical methods

Code written for Applied Computer Science **Numerical methods** course at [AGH UST](https://www.agh.edu.pl/en) [WFiIS](https://www.fis.agh.edu.pl/en/).

Semester `4`, year `2021`.

## Tools used during the course

`Makefile`:

```make
CXX = gcc
EXEC = test
CXXFLAGS += -pedantic -Wall -Wno-unused-variable
LFLAGS += -lm

SRC=$(wildcard *.c)
OBJ=$(SRC:.c=.o)
DEP=$(SRC:.c=.d)

.PHONY: all run clean

all: $(EXEC) run

$(EXEC): $(OBJ) 
	@$(CXX) $^ -o $@ $(LFLAGS)

$(OBJ): $(SRC)
	@$(CXX) -c $^ $(CXXFLAGS)

-include $(DEP)

run:
	@$(EXEC)

clean:
	rm -f $(EXEC) $(OBJ) $(DEP)
```

`CMakeLists.txt` (for GSL):

```cmake
cmake_minimum_required(VERSION 3.19)
project(nm2021 C)

#----------------------------------------------------------------------------

set(CMAKE_COLOR_MAKEFILE ON)
set(CMAKE_C_FLAGS "-Wall -pedantic -g")

#----------------------------------------------------------------------------

set(PROJECT_LINK_DIRECTORY ${PROJECT_SOURCE_DIR})

#----------------------------------------------------------------------------
# Create library
# --- implicite ---
file(GLOB SOURCES "${PROJECT_SOURCE_DIR}/*.c")

# --- explicite ---
set(GSL_ROOT_DIR #[[Your_GSL_Directory]])
find_package(GSL REQUIRED)
# add_library(CPPLabSolution SHARED MyList.cpp)

#----------------------------------------------------------------------------
# Create executable
add_executable(nmexe ${SOURCES})
target_link_libraries(nmexe PUBLIC GSL::gsl GSL::gslcblas)
```
  
## License

Sources are licensed under MIT, a free and open-source license. For details, please see [the license file](LICENSE.md).
