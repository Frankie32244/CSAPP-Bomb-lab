## CSAPP bomb lab TODOs & Updates
- [X] phase1  
- [X] phase2  
- [X] phase3  
- [X] phase4
- [ ] phase5
- [ ] phase6 

## example : phase_2() analysis
```linux
; 综合下述分析，phase_2() 的答案 为六个数字 -- 1 2 4 8 16 32 
0000000000400efc <phase_2>:
  400efc:	55                   	push   %rbp
  400efd:	53                   	push   %rbx
  400efe:	48 83 ec 28          	sub    $0x28,%rsp
  400f02:	48 89 e6             	mov    %rsp,%rsi
  400f05:	e8 52 05 00 00       	call   40145c <read_six_numbers>  ; 读取6个数
  400f0a:	83 3c 24 01          	cmpl   $0x1,(%rsp)                ; 比较第一个数和 1 的结果
  400f0e:	74 20                	je     400f30 <phase_2+0x34>      ; 如果第一个数是1， 跳转0x400f30
  400f10:	e8 25 05 00 00       	call   40143a <explode_bomb>      ; 不是1 则爆炸
  400f15:	eb 19                	jmp    400f30 <phase_2+0x34>      ; 是1，跳到400f30
  400f17:	8b 43 fc             	mov    -0x4(%rbx),%eax            ; $rbx - 4 地址的数值给%eax ,也就是%eax = 1
  400f1a:	01 c0                	add    %eax,%eax                  ; $eax + 1 也就是 $eax = 2 
  400f1c:	39 03                	cmp    %eax,(%rbx)                ; 比较 $eax 和 $rbx 值是否相等，意思就是$rbx 所指向的值得为2
  400f1e:	74 05                	je     400f25 <phase_2+0x29>      ; 相等则跳到 0x400f25
  400f20:	e8 15 05 00 00       	call   40143a <explode_bomb>      ; 不等于2 则爆炸
  400f25:	48 83 c3 04          	add    $0x4,%rbx                  ; $ rbx + 4
  400f29:	48 39 eb             	cmp    %rbp,%rbx                  ; 比较 $rbp $rbx，也就是while 循环的限制条件
  400f2c:	75 e9                	jne    400f17 <phase_2+0x1b>      ; 还符合循环条件
  400f2e:	eb 0c                	jmp    400f3c <phase_2+0x40>      ; 跳出循环
  400f30:	48 8d 5c 24 04       	lea    0x4(%rsp),%rbx             ; $rsp 指针 + 4 所指向的值给%rbx
  400f35:	48 8d 6c 24 18       	lea    0x18(%rsp),%rbp            
  400f3a:	eb db                	jmp    400f17 <phase_2+0x1b>      ; 跳到400f17
  400f3c:	48 83 c4 28          	add    $0x28,%rsp                 ; 栈指针 $rsp + 28 
  400f40:	5b                   	pop    %rbx
  400f41:	5d                   	pop    %rbp
  400f42:	c3                   	ret    

```
## Referrence
* Ref1: [CMU CSAPP-labs-handout](http://csapp.cs.cmu.edu/3e/labs.html)
* Ref2: [bomb lab_solution_video-by-guoguo](https://www.bilibili.com/video/BV1vu411o7QP/)
* Ref3: [周小伦CSAPP-bomb-lab](https://zhuanlan.zhihu.com/p/339461318)

