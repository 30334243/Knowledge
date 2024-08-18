~~~
std::string *str{new std::string{"Hello Word"}};
str[0] = '?';
if (str->size() == 1)
    std::cout << str[0] << std::endl;
return 0;
~~~
Вывод "?"

В пямяти
~~~
0000027DE6D1A970  3F 00 6C 6C 6F 20 57 6F 72 64 00 00 00 00 00 00  ?.llo Word......  
0000027DE6D1A980  01 00 00 00 00 00 00 00 0F 00 00 00 00 00 00 00  ................  
~~~
Ассемблерный листинг
~~~
mov qword ptr ss:[rsp+10],rbx
push r14
sub rsp,20
mov ecx,20
call shared_ptr.7FF6F8BB17A0
mov rbx,rax
mov qword ptr ss:[rsp+30],rax
mov r14d,A
test rax,rax
je shared_ptr.7FF6F8BB1700
xorps xmm0,xmm0
movups xmmword ptr ds:[rax],xmm0
mov qword ptr ds:[rax+10],r14
mov qword ptr ds:[rax+18],F
mov r8d,r14d
lea rdx,qword ptr ds:[7FF6F8BB3398]
mov rcx,rax
call <JMP.&memcpy>
mov byte ptr ds:[rbx+A],0
mov ecx,20
call shared_ptr.7FF6F8BB17A0
mov rbx,rax
mov qword ptr ss:[rsp+30],rax
test rax,rax
je shared_ptr.7FF6F8BB1741
xorps xmm0,xmm0
movups xmmword ptr ds:[rax],xmm0
mov qword ptr ds:[rax+10],r14
mov qword ptr ds:[rax+18],F
mov r8,r14
lea rdx,qword ptr ds:[7FF6F8BB3398]
mov rcx,rax
call <JMP.&memcpy>
mov byte ptr ds:[rbx+A],0
jmp shared_ptr.7FF6F8BB1743
xor ebx,ebx
mov qword ptr ds:[rbx+10],1
mov rax,rbx
cmp qword ptr ds:[rbx+18],F
jbe shared_ptr.7FF6F8BB1758
mov rax,qword ptr ds:[rbx]
mov word ptr ds:[rax],3F
cmp qword ptr ds:[rbx+10],1
jne shared_ptr.7FF6F8BB1783
~~~
В строке `mov qword ptr ds:[rbx+10],1` происходит затирание текущего размера на 1
