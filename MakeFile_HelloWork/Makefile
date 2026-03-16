all:
	gcc -E main.c -o main.i
	gcc -S main.i -o main.s
	as main.s -o main.o
	gcc -v -o main main.o