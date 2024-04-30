# $Id $

# Makefile for Rom24. Works fine on my Debian system.
# You may need to use 'gmake' on BSD systems.

CC = gcc
RM = rm
EXE = ../area/rom
LIB = ../area/libmud.a
PROF = -O -g3

OS_TYPE := $(shell uname)


C_FLAGS = $(PROF) -Wall

# Macos doesn't use the crypt library, instead it defines crypt in unistd.h
ifeq ($(OS_TYPE),Darwin)
L_FLAGS = $(PROF)
else
L_FLAGS = $(PROF) -lcrypt
endif

#IMC2 - Comment out to disable IMC2 support
IMC = 1

ifdef IMC
   C_FLAGS := $(C_FLAGS) -DIMC -DIMCROM
endif

# Source Files
SRC_FILES := $(wildcard *.c)

# Object Files
OBJ_DIR = obj
OBJ_FILES := $(patsubst %.c,$(OBJ_DIR)/%.o,$(SRC_FILES))

# Make the Object directory if it doesn't exist
$(shell   mkdir -p $(OBJ_DIR))

rom: clean $(OBJ_FILES)
	$(RM) -f $(EXE)
	$(CC) -o $(EXE) $(OBJ_FILES) $(L_FLAGS)


lib: C_FLAGS := $(C_FLAGS) -DAS_LIB
lib: clean $(OBJ_FILES)
	$(RM) -f $(LIB)
	ar rcs $(LIB) $(OBJ_FILES)

$(OBJ_DIR)/%.o: %.c
	$(CC) $(C_FLAGS) -c -o $@ $<

clean:
	$(RM) -f $(OBJ_FILES) $(EXE) *~ *.bak *.orig *.rej

distro:
	make clean
	cd ../..
	$(RM) -f log/*.log
	tar zvcf quickmud-`date -I`.tar.gz QuickMUD
