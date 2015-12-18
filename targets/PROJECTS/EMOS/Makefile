#include $(OPENAIR_HOME)/common/utils/Makefile.inc
SRC = dump_size.c 

CFLAGS += -std=gnu99 
CFLAGS += -mmmx -msse -msse2 -mssse3 -msse4.1

CFLAGS += -I$(OPENAIR1_DIR) -I$(OPENAIR2_DIR)/RRC/LITE/MESSAGES -I$(OPENAIR_HOME)/common/utils -I$(OPENAIR2_DIR) -I$(OPENAIR2_DIR)/COMMON -I$(OPENAIR2_DIR)/RRC/

CFLAGS += -DNB_ANTENNAS_RX=2 -DNB_ANTENNAS_TXRX=2 -DNB_ANTENNAS_TX=2

CFLAGS += -DEMOS -DEXMIMO -DNO_RTAI

ifeq ($(EMOS_CHANNEL),1)
CFLAGS += -DEMOS_CHANNEL
endif

all: dump_size cstruct

$(OBJ): %.o : %.c
	@echo Compiling $< ...
	@$(CC) -c $(CFLAGS) -o $@ $<

cstruct: cstruct.c MatlabCStruct.c
	mkoctfile --mex cstruct.c MatlabCStruct.c

dump_size: dump_size.c
	$(CC) $(CFLAGS) $(LDFLAGS) dump_size.c -o dump_size

cleanall: clean
	rm -rf dump_size cstruct.oct cstruct.mex

clean:
	rm *.o

show:
	@echo $(CFLAGS)

beautiful:
	astyle --style=gnu -s2 $(SRC)
