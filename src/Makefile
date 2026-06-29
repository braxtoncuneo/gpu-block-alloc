NVCC       := nvcc
NVCC_FLAGS := -std=c++17 -x=cu --forward-unknown-to-host-compiler -g

HEADERS := allocator.h log.h typedAlloc.h Makefile
INTR := intr/atomic.h intr/bitwise.h

all: main.exe paraTest.exe gpuTest.exe


gpuTest.exe: gpuTest.cu $(HEADERS) $(INTR)
	$(NVCC) $(NVCC_FLAGS) $(filter-out $(HEADERS),$^) -o $@

main.exe: main.cu $(HEADERS) $(INTR)
	$(NVCC) $(NVCC_FLAGS) $< -o $@

paraTest.exe: paraTest.cu log.cpp $(HEADERS) $(INTR)
	$(NVCC) $(NVCC_FLAGS) $(filter-out $(HEADERS),$^) -o $@

run: main.exe paraTest.exe
	./main.exe
	./paraTest.exe
	./gpuTest.exe

run-main: main.exe
	./main.exe

run-para: paraTest.exe
	./paraTest.exe

run-gpu:  gpuTest.exe
	./gpuTest.exe

clean:
	rm -f main.exe paraTest.exe

.PHONY: all run run-main run-para clean
