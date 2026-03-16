PROJECT_NAME := sum
OBJ_FILE = Out/main.o Out/sum.o

Out/main.o : Src/main.c
	@gcc -c -I./Inc Src/main.c -o Out/main.o
Out/sum.o : Src/sum.c
	@gcc -c -I./Inc Src/sum.c -o Out/sum.o
.PHONY: build
build: $(OBJ_FILE)
	@gcc $(OBJ_FILE) -o Out/main.exe
	@echo "Build Done!"

.PHONY: target
target:
	Out/main.exe

.PHONY: clean
clear:
	@rm ./Out/*.o
	@echo "Clear all out file"