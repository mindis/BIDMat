include Makefile.incl

MKL_OBJS=BIDMat_CBLAS.$(OBJ) BIDMat_UTILS.$(OBJ) BIDMat_SPBLAS.$(OBJ) BIDMat_LAPACK.$(OBJ) \
         BIDMat_VML.$(OBJ) BIDMat_VSL.$(OBJ)

CUDA_OBJS=BIDMat_CUMAT.$(OBJ) MatKernel.$(OBJ)

.SUFFIXES: .$(OBJ) .c .cpp .cu

all: $(LIBPREPEND)bidmatcuda$(LIBAPPEND) $(LIBPREPEND)bidmatmkl$(LIBAPPEND) 

$(LIBPREPEND)bidmatmkl$(LIBAPPEND): $(MKL_OBJS)
	$(LD) $(LDFLAGS) $(MKL_OBJS) $(MKL_LIBS) $(OUTFLG)$@

$(LIBPREPEND)bidmatcuda$(LIBAPPEND): $(CUDA_OBJS)
	$(GLD) $(LDFLAGS) $(CUDA_OBJS) $(CUDA_LIBS) $(OUTFLG)$@

%.$(OBJ) : %.c
	$(CC) $(LAPACK_INCLUDES) $(CFLAGS) $*.c

%.$(OBJ) : %.cpp
	$(GCC) $(CPPFLAGS) $(LAPACK_INCLUDES) $*.cpp

%.$(OBJ) : %.cu
	$(NVCC) $(NVCCFLAGS) $*.cu

install: all
	cp $(LIBPREPEND)bidmatcuda$(LIBAPPEND) $(INSTALL_DIR)
	cp $(LIBPREPEND)bidmatmkl$(LIBAPPEND)  $(INSTALL_DIR)
	cp $(LIBPREPEND)bidmatcuda$(LIBAPPEND) $(INSTALL_DIR)/../../BIDMach/lib
	cp $(LIBPREPEND)bidmatmkl$(LIBAPPEND)  $(INSTALL_DIR)/../../BIDMach/lib

clean:
	rm -f *.$(OBJ) *$(LIBAPPEND) *.pdb *.exp *.lib

distclean: clean
	rm -f *$(LIBAPPEND) *.exp *.lib *.jnilib Makefile.incl

