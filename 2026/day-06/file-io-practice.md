~$ touch notes.txt
~$ echo "hello world" > notes.txt
~$ echo "line 2 text" >> notes.txt
~$ echo "3 lines done" > notes.txt
~$ cat notes.txt
3 lines done
~$ head notes.txt
3 lines done
~$ echo "more..." | tee notes.txt
more...
~$ cat notes.txt
more...