CC		:= gcc
CFLAGS	:= -Wall -Wextra -g  -lm
LDFLAGS := `sdl-config --libs --cflags`
BIN		:= bin
SRC		:= src
INCLUDE	:= include
LIB		:= lib
LIBRARIES	:=

ifeq ($(OS),Windows_NT)
EXECUTABLE	:= main.exe
else
EXECUTABLE	:= main
endif

SOURCEDIRS	:= $(shell find $(SRC) -type d)
INCLUDEDIRS	:= $(shell find $(INCLUDE) -type d)
LIBDIRS		:= $(shell find $(LIB) -type d)

CINCLUDES	:= $(patsubst %,-I%, $(INCLUDEDIRS:%/=%))
CLIBS		:= $(patsubst %,-L%, $(LIBDIRS:%/=%))

SOURCES		:= $(wildcard $(patsubst %,%/*.c, $(SOURCEDIRS)))
OBJECTS		:= $(SOURCES:.c=.o)

#       SDL options
CC_SDL=-I/usr/local/include/SDL -D_REENTRANT
LN_SDL=-L/usr/local/lib -Wl,-rpath,/usr/local/lib -lSDL -lSDL_image -lpthread 

all: $(BIN)/$(EXECUTABLE)

.PHONY: clean
clean:
	-$(RM) $(BIN)/$(EXECUTABLE)
	-$(RM) $(OBJECTS)


run: all
	./$(BIN)/$(EXECUTABLE)

$(BIN)/$(EXECUTABLE): $(OBJECTS)
	$(CC) $(CFLAGS) $(CINCLUDES) $(CLIBS) $^ $(LDFLAGS) -o $@ $(LIBRARIES)