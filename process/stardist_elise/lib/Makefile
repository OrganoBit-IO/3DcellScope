UNAME := $(shell uname)

ifeq ($(UNAME), Linux)
	LIB=libstardist3d.so
	CFLAGSQHULL=-fPIC -O3
	CFLAGSLIB=-shared -fPIC
else ifeq ($(UNAME), Darwin)
	LIB=libstardist3d.dylib
	CFLAGSQHULL=-O3 
	CFLAGSLIB=-dynamiclib 
endif

CFLAGS=-std=c++11 -O3 -I/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/include/python3.9 -I/Users/domi/OrganoBit/dev_zone/3DcellScope/.venv/lib/python3.9/site-packages/numpy/core/include -undefined dynamic_lookup
BUILDDIR=build


all: lib

qhull_cpp:
	mkdir -p $(BUILDDIR) && cd $(BUILDDIR) && $(CXX) -c $(CFLAGSQHULL) -fpermissive -I../qhull_src/src/ ../qhull_src/src/libqhullcpp/*.cpp 

qhull_c:
	mkdir -p $(BUILDDIR) && cd $(BUILDDIR) && $(CC) -c $(CFLAGSQHULL) -I../qhull_src/src/ ../qhull_src/src/libqhull_r/*.c

lib: qhull_c qhull_cpp stardist3d.cpp stardist3d_impl.cpp stardist3d_lib.c utils.cpp 
	$(CXX) $(CFLAGSLIB) $(CFLAGS) -o $(LIB) stardist3d.cpp stardist3d_impl.cpp stardist3d_lib.c utils.cpp -I./qhull_src/src/ $(BUILDDIR)/*.o 

lib2d: clipper.cpp stardist2d.cpp utils.cpp
	$(CXX) $(CFLAGSLIB) $(CFLAGS) -o libstardist2d.dylib clipper.cpp stardist2d.cpp utils.cpp 

