ROOT = ../..

include $(ROOT)/common/Makefile.common

ALGO_O = herlihy.o
ALGO_C = herlihy.c

BINS = "$(BINDIR)/lb-sl_herlihy$(BIN_SUFFIX)"
PROF = $(ROOT)/src

.PHONY:	all clean

all:	main

measurements.o:
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/measurements.o $(PROF)/measurements.c

skiplist-lock.o: 
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/skiplist-lock.o skiplist-lock.c

herlihy.o: skiplist-lock.h skiplist-lock.o 
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/herlihy.o herlihy.c

intset.o: skiplist-lock.h herlihy.h 
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/intset.o intset.c

test.o: skiplist-lock.h herlihy.h intset.h
	$(CC) $(CFLAGS) -c -o $(BUILDIR)/test.o $(TEST_FILE)

main: measurements.o skiplist-lock.o herlihy.o intset.o test.o 
	$(CC) $(CFLAGS) $(BUILDIR)/measurements.o $(BUILDIR)/skiplist-lock.o $(BUILDIR)/herlihy.o $(BUILDIR)/intset.o $(BUILDIR)/test.o -o $(BINS) $(LDFLAGS) 

clean:
	rm -f $(BINS)
