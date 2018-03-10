CGC := psp2cgc
CGCFLAGS := -Wperf -fastprecision -O3

SHSRC := $(wildcard *.cg)
SHBIN := $(SHSRC:.cg=.gxp)

all: $(SHBIN)

%_f.gxp: %_f.cg
	$(CGC) -profile sce_fp_psp2 $< $(CGCFLAGS) -o $@

%_v.gxp: %_v.cg
	$(CGC) -profile sce_vp_psp2 $< $(CGCFLAGS) -o $@

clean:
	rm -f *.gxp
