#### Find and print the main{} function in C files 

$grep -Pzo "(?s)^(\s*)\N*main.*?{.*?^\1}" *.c

https://stackoverflow.com/a/7167115
