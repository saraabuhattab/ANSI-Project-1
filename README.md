# ANSI-project1
Counts the number of characters in a string and the number of lowercase letters

%include "asm_io.inc"
SECTION .data
string: db "Hello World ",10,0
strlen: db "the length of the string is ",0
upper: db "the number of lower case letters is ",0
error: db "too many characters",10,0

SECTION .text
   global asm_main
asm_main:

   push ebp                  ; calling convention
   mov ebp, esp

   mov ebx, string
   mov ecx, 0 ;lowercase
   mov edx, 0 ;all letters

comparing:

  cmp byte [ebx], 'a'
  jb next 
  cmp byte [ebx], 'z'
  ja next
  inc ecx
  inc edx
  inc ebx
  cmp edx, 20
  jge message
  cmp byte[ebx], 0 ;
  jne comparing ; if not at end go back
  jmp body

next:
  inc edx
  inc ebx 
  cmp edx, 20
  jge message
  cmp byte[ebx], 0 ;
  jne comparing ; if not at end go back

body:
  cmp edx, 20
  jge message
  mov eax, string ; moves and prints necessary strings with values after them
  call print_string
  mov eax,strlen
  call print_string
  mov eax, edx
  dec eax
  call print_int
  call print_nl
  mov eax,upper
  call print_string
  mov eax,ecx
  call print_int
  jmp end

message:

  mov eax, error
  call print_string
  jmp end
   

end:

   mov esp, ebp              ; returning convention
   pop ebp                   ; same as "leave" op

   mov eax,0                 ; normal (no error) return value
   ret                       ; return



  
