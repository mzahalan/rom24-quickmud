# $Id $

# Makefile for Rom24. Works fine on my Debian system.
# You may need to use 'gmake' on BSD systems.

CC = gcc
RM = rm
EXE = ../area/rom
PROF = -O -g3

C_FLAGS = $(PROF) -Wall
L_FLAGS = $(PROF)

# For Linux we want to add -lcrypt, but not for OSX (Darwin)
# Note - This likely does not work on Windows (no uname)
# To Guard for Windows see this:
# https://stackoverflow.com/questions/714100/os-detecting-makefile
#
UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Linux)
    L_FLAGS += -lcrypt
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

rom: $(OBJ_FILES)
	$(RM) -f $(EXE)
	$(CC) -o $(EXE) $(OBJ_FILES) $(L_FLAGS)

$(OBJ_DIR)/%.o: %.c
	$(CC) $(C_FLAGS) -c -o $@ $<

clean:
	$(RM) -f $(OBJ_FILES) $(EXE) *~ *.bak *.orig *.rej

distro:
	make clean
	cd ../..
	$(RM) -f log/*.log
	tar zvcf quickmud-`date -I`.tar.gz QuickMUD
