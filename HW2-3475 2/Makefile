#Saik Jalal
#CSE375
#Programming Assignment #2 - Kmeans

TARGETS = kmeans-serial kmeans-parallel
 # Kmeans-parallel generates the executable for the parallel version
 # TODO: put your file names here, *without a file extension*

# names of .cc files that are used by all of the above targets
CXXFILES = # no common files yet :)
#DATASET = datasets/dataset1.ext  # No dataset dependency for kmeans-serial
#
# The rest of this file should never need to change
#

# Let the programmer choose 32 or 64 bits, but default to 64 bits
BITS ?= 64

# Specify the name of the folder where all output will go
ODIR := ./obj$(BITS)

# This line ensures that the above folder will be created before any compiling
# happens.
output_folder := $(shell mkdir -p $(ODIR))

# Generate the names of the .o files and .exe files that we will be creating.
# Note that we name all .o files explicitly, so that we can add them to the
# .PRECIOUS target, which prevents them from being auto-removed.
COMMONOFILES = $(patsubst %, $(ODIR)/%.o, $(CXXFILES)) # NB: These get linked into every executable
ALLOFILES    = $(patsubst %, $(ODIR)/%.o, $(CXXFILES) $(TARGETS))
EXEFILES     = $(patsubst %, $(ODIR)/%.exe, $(TARGETS))

# Generate the names of the dependency files that g++ will generate, so that we
# can include them later in this makefile
DFILES     = $(patsubst %.o, %.d, $(ALLOFILES))

# Basic tool configuration for gcc/g++.  We will create debug symbols, enable
# optimizations, and generate dependency information on-the-fly
CXX      = g++
LD       = g++
# NB: On the next line, the extra "-I" part is only needed on the Lehigh CSE
#     SunLab.  If you are using Docker, it won't cause trouble to have it, but 
#     it won't do anything
CXXFLAGS  = -MMD -O3 -ggdb -std=c++23 -Wall -Wextra -Werror -Wno-unused-parameter $(CXXEXTRA) -I/usr/include/openssl3
# NB: On the next line, Docker is fine with `-lcrypto`, but that doesn't work on
#     SunLab.  The more explicit `-l:libcrypto.so.3` works on Docker and SunLab.
LDFLAGS   = -lpthread -l:libcrypto.so.3 -ldl $(LDEXTRA)

# Build 'all' by default, and don't clobber .o files after each build
.DEFAULT_GOAL = all
.PRECIOUS: $(ALLOFILES)
.PHONY: all clean

# Goal is to build all executables
all: $(EXEFILES)

# Rules for building object files
$(ODIR)/%.o: %.cc
	@echo "[CXX] $< --> $@"
	@$(CXX) $< -o $@ -c $(CXXFLAGS)

# Rules for building executables... we assume an executable uses *all* of the 
# common OFILES
$(ODIR)/%.exe: $(ODIR)/%.o $(COMMONOFILES)
	@echo "[LD] $^ --> $@"
	@$(CXX) $^ -o $@ $(LDFLAGS)

# clean by clobbering the build folder
clean:
	@echo Cleaning up...
	@rm -rf $(ODIR)

# Include any dependencies we generated previously
-include $(DFILES)

#FOR TBB
export LD_LIBRARY_PATH=/home/saj325/oneapi-tbb-2021.8.0/lib/intel64/gcc4.8