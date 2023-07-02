CC =gcc -Wall -Werror -Wextra -std=c11 -D_GNU_SOURSE

all: s21_math.a test gcov_report clean

s21_math.a:
	$(CC) -c s21_math.c -o./s21_math.o
	ar rcs s21_math.a s21_math.o
	ranlib s21_math.a
clean:
	rm -rf *.o *.gcda *.gcno *.a *.out *.info
test: s21_math.a
	$(CC) test.c -L. s21_math.a -lcheck -lm -lpthread --coverage -o ./test.out
	./test.out

gcov_report: s21_math.a
	$(CC) --coverage test.c s21_math.c s21_math.a -L. s21_math.a -lcheck -lm -lpthread -o ./test.out
	./test.out
	lcov -t "my_test" -c -d ./ --output-file ./test.info
	genhtml -o report test.info
	rm -rf *.gcda *.gcno *.out
rebuild:
	make clean
	make
leaks:
	leaks -atExit -- ./test.out
