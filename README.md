# Tools

### 2016/02/28
> 蓝灯补丁更新，支持 2.1.0

> * 去启动弹窗  
> * 便携化配置
> * 单进程

> 请到 releases 下载


代码修改:

```asm
; 2.1.0 以上去弹窗

00404358   .  E8 E3860000          CALL 0040CA40
0040435D   .  803D D5B0B500 00     CMP BYTE PTR [0B5B0D5],0
00404364   .  74 17                JE SHORT 0040437D
00404366   .  8B1D 685A0B01        MOV EBX,DWORD PTR [10B5A68]
0040436C   .  0FB61B               MOVZX EBX,BYTE PTR [EBX]
0040436F   .  80FB 00              CMP BL,0
00404372   .  75 09                JNE SHORT 0040437D                       ; JMP
00404374   .  E8 F7391500          CALL 00557D70
00404379  />  83C4 30              ADD ESP,30
0040437C  \.  C3                   RETN
0040437D   >  C70424 20917A00      MOV DWORD PTR [ESP],007A9120
00404384   .  E8 97350100          CALL 00417920                            ; [lantern.00417920
00404389   .  8B5C24 04            MOV EBX,DWORD PTR [ESP+4]
0040438D   .  83FB 00              CMP EBX,0
00404390   .  0F84 BD000000        JE 00404453


0F B6 1B 80 FB 00 75 09


; 单进程

8B 4C 24 ?? 8B 5C 24 ?? 83 FB 00 0F 84 ?? ?? ?? ?? 89 84 24 ?? ?? ?? ??
8B 4C 24 ?? 8B 5C 24 ?? 83 FB 00 90 E9 ?? ?? ?? ?? 89 84 24 ?? ?? ?? ??


00552E3A      8B4C24 58     mov ecx,dword ptr [esp+58]
00552E3E      8B5C24 54     mov ebx,dword ptr [esp+54]
00552E42      83FB 00       cmp ebx,0
00552E45      0F84 F7030000 je lantern_.00553242
00552E4B      898424 C80000>mov dword ptr [esp+C8],eax
00552E52      8943 38       mov dword ptr [ebx+38],eax
00552E55      898C24 CC0000>mov dword ptr [esp+CC],ecx
00552E5C      803D BCBE0301>cmp byte ptr [103BEBC],0


00552E3A   > /8B4C24 58     mov ecx,dword ptr [esp+58]
00552E3E   . |8B5C24 54     mov ebx,dword ptr [esp+54]
00552E42     |83FB 00       cmp ebx,0
00552E45     |90            nop
00552E46     |E9 F7030000   jmp lantern_.00553242
00552E4B   > |898424 C80000>mov dword ptr [esp+C8],eax
00552E52   . |8943 38       mov dword ptr [ebx+38],eax
00552E55   . |898C24 CC0000>mov dword ptr [esp+CC],ecx
00552E5C   . |803D BCBE0301>cmp byte ptr [103BEBC],0

; 去掉pac

0F B6 5C 24 ?? 80 FB 00 0F 84 ?? ?? ?? ?? E8 ?? ?? ?? ?? BB
0F B6 5C 24 ?? 80 FB 00 90 E9 ?? ?? ?? ?? E8 ?? ?? ?? ?? BB

00404323   .  0FB65C24 04   movzx ebx,byte ptr [esp+4]
00404328   .  80FB 00       cmp bl,0
0040432B      0F84 29010000 je lantern.0040445A
00404331   .  E8 DA140000   call lantern.00405810
00404336   >  BB F4889700   mov ebx,lantern.009788F4

```





