# BEGIN_ICS_COPYRIGHT8 ****************************************
# 
# Copyright (c) 2015-2017, Intel Corporation
# 
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
# 
#     * Redistributions of source code must retain the above copyright notice,
#       this list of conditions and the following disclaimer.
#     * Redistributions in binary form must reproduce the above copyright
#       notice, this list of conditions and the following disclaimer in the
#       documentation and/or other materials provided with the distribution.
#     * Neither the name of Intel Corporation nor the names of its contributors
#       may be used to endorse or promote products derived from this software
#       without specific prior written permission.
# 
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE
# FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
# DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
# SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
# CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
# OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
# 
# END_ICS_COPYRIGHT8   ****************************************
# Makefile for SM Module

# Include Make Control Settings
include $(TL_DIR)/$(PROJ_FILE_DIR)/Makesettings.project

#=============================================================================#
# Definitions:
#-----------------------------------------------------------------------------#

# Name of SubProjects
DS_SUBPROJECTS	=
# name of executable or downloadable image
EXECUTABLE		= $(BUILDDIR)/eepha$(EXE_SUFFIX)
# list of sub directories to build
DIRS			=
# C files (.c)
CFILES			= 	eepha_eostl.c \
					eepha_util.c \
					eepha_vesw_fsm.c \
					eepha_process_mad.c \
					eepha_process_eeph_msg.c \
					eepha_diag_ctrl.c \
					eepha_xml.c \
					eepha_cpi.c \
					eepha_gen_info.c
				# Add more c files here
ifeq ($(BUILD_TARGET_OS),VXWORKS)
CFILES			+= eepha_vxworks.c
else
CFILES			+= eepha_linux.c
endif

# C++ files (.cpp)
CCFILES			= \
				# Add more cpp files here
# lex files (.lex)
LFILES			= \
				# Add more lex files here
# archive library files (basename, $ARFILES will add MOD_LIB_DIR/prefix and suffix)
LIBFILES = 
# Windows Resource Files (.rc)
RSCFILES		=
# Windows IDL File (.idl)
IDLFILE			=
# Windows Linker Module Definitions (.def) file for dll's
DEFFILE			=
# targets to build during INCLUDES phase (add public includes here)
INCLUDE_TARGETS	= \
				# Add more h hpp files here
# Non-compiled files
MISC_FILES		= 
# all source files
SOURCES			= $(CFILES) $(CCFILES) $(LFILES) $(RSCFILES) $(IDLFILE)
# Source files to include in DSP File
DSP_SOURCES		= $(INCLUDE_TARGETS) $(SOURCES) $(MISC_FILES) \
				  $(RSCFILES) $(DEFFILE) $(MAKEFILE)
# all object files
OBJECTS			= $(CFILES:.c=$(OBJ_SUFFIX)) $(CCFILES:.cpp=$(OBJ_SUFFIX)) \
				  $(LFILES:.lex=$(OBJ_SUFFIX))
RSCOBJECTS		= $(RSCFILES:.rc=$(RES_SUFFIX))
# targets to build during LIBS phase
LIB_TARGETS_IMPLIB	=
ifeq ($(BUILD_TARGET_OS),VXWORKS)
LIB_TARGETS_ARLIB	= $(LIB_PREFIX)eepha$(ARLIB_SUFFIX)
endif
LIB_TARGETS_EXP		= $(LIB_TARGETS_IMPLIB:$(ARLIB_SUFFIX)=$(EXP_SUFFIX))
LIB_TARGETS_MISC	= 
# targets to build during CMDS phase
CMD_TARGETS_SHLIB	= 
CMD_TARGETS_EXE		= $(EXECUTABLE)
CMD_TARGETS_MISC	=
# files to remove during clean phase
CLEAN_TARGETS_MISC	=  
CLEAN_TARGETS		= $(OBJECTS) $(RSCOBJECTS) $(IDL_TARGETS) $(CLEAN_TARGETS_MISC)
# other files to remove during clobber phase
CLOBBER_TARGETS_MISC=
# sub-directory to install to within bin
BIN_SUBDIR		= 
# sub-directory to install to within include
INCLUDE_SUBDIR		=

# Additional Settings

ifeq ($(BUILD_TARGET_OS),VXWORKS)
CLOCAL = $(CPIE) -xc
else
CLOCAL = $(CPIE)
endif

LIB_DIRS += /usr/lib64

LOCAL_INCLUDE_DIRS = $(MOD_DIR)/src/smi/include $(OPENIB_USER_LIB_DIRS) $(MOD_DIR)/include

LOCALDEPLIBS =$(IBACCESS_USER_LIBS) if3 if3sa net cs mai ibaccess config vslogu public Xml opamgt-priv
LOCALLIBS=$(OPENIB_USER_LIBS) m rt crypto
LOCAL_LIB_DIRS=$(OPENIB_USER_LIB_DIRS) $(IBACCESS_USER_LIB_DIRS)

ifneq "$(BUILD_TARGET_OS)" "VXWORKS"
LOCALLIBS+= expat
endif
#CLOCAL  += -DEEPH_DEMO -DDEBUG_EEPHA

# Include Make Rules definitions and rules
include $(PROJ_SM_DIR)/Makerules.module
#include $(TL_DIR)/Esm/ib/Makerules.module

#=============================================================================#
# Overrides:
#-----------------------------------------------------------------------------#
#CCOPT			=	# C++ optimization flags, default lets build config decide
#COPT			=	# C optimization flags, default lets build config decide
#SUBSYSTEM = Subsystem to build for (none, console or windows) [none]
#					 (Windows Only)
#USEMFC	= How Windows MFC should be used (none, static, shared, no_mfc) [none]
#				(Windows Only)
#=============================================================================#

#=============================================================================#
# Rules:
#-----------------------------------------------------------------------------#
# process Sub-directories
include $(TL_DIR)/Makerules/Maketargets.toplevel

# build cmds and libs
include $(TL_DIR)/Makerules/Maketargets.build

# install for includes, libs and cmds phases
include $(TL_DIR)/Makerules/Maketargets.install

# install for stage phase
#include $(TL_DIR)/Makerules/Maketargets.stage
STAGE::

# Unit test execution
#include $(TL_DIR)/Makerules/Maketargets.runtest

clobber:: clobber_module

#=============================================================================#

#=============================================================================#
# DO NOT DELETE THIS LINE -- make depend depends on it.
#=============================================================================#
