EXECUTABLE = arap_mesh_deformation
OBJS = build/LandMark.o build/LandMarkSet.o build/CUDAWarpingSolver.o build/mLibSource.o build/main.o build/WarpingSolver.o build/CeresSolver.o

UNAME := $(shell uname)
ifeq ($(UNAME), Darwin)
  LFLAGS += -L../external/OpenMesh/lib/osx -Wl,-rpath,../external/OpenMesh/lib/osx
endif

ifeq ($(UNAME), Linux)
  LFLAGS += -L../external/OpenMesh/lib/linux -Wl,-rpath,../external/OpenMesh/lib/linux
endif

LFLAGS += -lOpenMeshCore -lOpenMeshTools

# # This should point to place where you unpacked or cloned Ceres.
# CERES_SRC_DIR := /home/xxuan/Desktop/optlang/Opt/examples/external/ceres-solver

# # This should point to the place where you built Ceres. If you got Ceres by
# # installing it, then this will likely be /usr/local/lib.
# CERES_BIN_DIR := /home/xxuan/Desktop/optlang/Opt/examples/external/ceres-bin

# # The place you unpacked or cloned Eigen. If Eigen was installed from packages,
# # this will likely be /usr/local/include.
# EIGEN_SRC_DIR := /usr/local/include/eigen3

# LFLAGS += -I$(CERES_SRC_DIR)/include \
#             -I$(EIGEN_SRC_DIR)

# LFLAGS += -lceres
# LFLAGS += -L$(CERES_BIN_DIR)/lib
# LFLAGS += -lgflags -lglog

# # If Ceres was built with Suitesparse:
# LFLAGS += -llapack -lcamd -lamd -lccolamd -lcolamd -lcholmod

# # If Ceres was built with CXSparse:
# LFLAGS += -lcxsparse

# # If Ceres was built with OpenMP:
# # LFLAGS += -fopenmp -lpthread -lgomp -lm -lz

include ../shared/make_template.inc
