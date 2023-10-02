#### CLion GDB debug fork()

In CLion to follow the child forked process

1. Set a break point at the beginning of your program (ie. the parent program, not the child program).
2. Start the program in the debugger.
3. Go to the debugger console (tab with the label gdb) in clion and enter `set follow-fork-mode child` and `set detach-on-fork off`.
4. Continue debugging.

<https://stackoverflow.com/a/49468112>