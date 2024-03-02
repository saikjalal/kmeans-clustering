#Saik Jalal
#CSE375
#Programming Assignment #2 - Kmeans

TARGETS = kmeans-serial kmeans-parallel

# Specify the name of the folder where all output will go
ODIR := ./obj$(BITS)

# Generate the names of the .o files and .exe files that we will be creating.
COMMONOFILES = $(patsubst %, $(ODIR)/%.o, $(CXXFILES))
ALLOFILES    = $(patsubst %, $(ODIR)/%.o, $(CXXFILES) $(TARGETS))
EXEFILES     = $(patsubst %, $(ODIR)/%.exe, $(TARGETS))

# Generate the names of the dependency files that g++ will generate
DFILES       = $(patsubst %.o, %.d, $(ALLOFILES))

# Basic tool configuration for gcc/g++
CXX      = g++
LD       = g++
CXXFLAGS = -MMD -O3 -ggdb -std=c++23 -Wall -Wextra -Wno-unused-parameter -fopenmp -I/usr/include/openssl3
LDFLAGS  = -lpthread -l:libcrypto.so.3 -ldl -fopenmp

# Build 'all' by default, and don't clobber .o files after each build
.DEFAULT_GOAL = all
.PRECIOUS: $(ALLOFILES)
.PHONY: all clean

# Goal is to build all executables
all: $(EXEFILES)

# Rules for building object files
$(ODIR)/%.o: %.cc | $(ODIR)
	@echo "[CXX] $< --> $@"
	@$(CXX) $< -o $@ -c $(CXXFLAGS)

# Rules for building executables
$(ODIR)/%.exe: $(ODIR)/%.o $(COMMONOFILES)
	@echo "[LD] $^ --> $@"
	@$(CXX) $^ -o $@ $(LDFLAGS)

# Create the output directory
$(ODIR):
	@mkdir -p $(ODIR)

# Clean by clobbering the build folder
clean:
	@echo Cleaning up...
	@rm -rf $(ODIR)

# Include any dependencies we generated previously
-include $(DFILES)