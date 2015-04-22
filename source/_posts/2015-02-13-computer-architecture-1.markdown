---
layout: post
title: "computer architecture 1"
date: 2015-02-13 14:28:43 -0500
comments: true
categories: computer_architecture
---

###charpter1
- What is computer architecture
    - 4 classes of computers
        - personal computer
        - server computer
        - embedded computer
        - supercomputer
 <!--more-->
    - What does “PostPC era” mean
        - personal mobile device(PMD)
        - cloud computing
            - server are replace by cloud computing
            - Software as a Service(Saas)
        - Portion of software run on a PMD, and a portion(part of) run in the cloud
        
    - What factors could affect performance
        - algorithm
        - programming language, compiler, architecture
        - processor and memory system
        - I/O system(including OS and hardware)
    
    - Eight great ideas – Know what they mean
        - 1.design for moore's law
        - 2.use abstraction to simplify design
        - 3.make the common case fast
        - 4.performance via parallelism
        - 5.performance via pipelining
        - 6.performance via prediction
        - 7.hierarchy of memory
        - 8.dependability via redundancy
   
- Different levels of program code
    - HLL -> Assembly language -> ML
    - 5 components of a computer
        - input
        - output
        - control
            - tells datapath, memory, I/O what to do according to the instructions.
        - datapath
            - performs the arithmetic operations
        - memory
    - input ->(control, datapath)->output
        
    - What is ISA?
        - instruction set architecture
            - the hardware/software interface
    
    - Understand “Yield” in terms of chip manufacturing?
        - Proportion of working dies per wafer晶圆(硅半导体集成电路制作所用的硅晶片)
    - Response time vs Throughput
        - Response time
            - How long it takes to do one task
        - Throughput
            - Total work done per unit time
            
        
    - Elapsed time vs CPU time
        - elapsed time
            - wall clock time
                - total response time, inkling everything
                - can be used to determine the system performance
        - cpu time
            - the time that cpu spent for **a given process**
            - can be divide into user CPU time and system CPU time
        
    - Know how to calculate CPU time, CPI_avg, IPC, Clock rate, Clock Cycle Time, and Performance
        - 1 cycle per second -> 1 Hz
            - 1 GHz = 10^9 hz
        - clock rate(frequency)
            - cycle per second
        - clock cycle time(period)        
            - duration of a clock cycle
        - CPU time
            - CPU time = CPU clock cycle * clock cycle time = CPU Clock cycle / Clock Rate
        - Instruction count
            - determine by program, ISA, compiler
        - Average cycle per instruction(CPI)
            - IPC = 1/CPI
        - Clock Cycle = Instruction * Average Cycle per instruction
        - CPU time = Instruction * CPI * Clock Cycle Time
            - = Instruction Count * CPI / Clock Rate
            - = Instruction Count / (Clock Rate * IPC)
            - = (Instruction/program) * (Cycles/Instruction) * (Seconds/Cycle)
            - = IC * PCI * CC
        - Clock Cycles = sum(CPI * Instruction Count)
        - how to measure performance
            - use instruction/second
                - so we can use the format clock rate/CPI
        - Performance depends on
            - Algorithm:affects IC, CPI
            - programming language: affects IC, CPI
            - Compiler:affects IC, CPI
            - ISA:affects IC, CPI, CC
        - if you want an improvement in the execution time
            - you need to deduce the percentage of old time
                - for example
                    - if you want to improve 50%, then you should use (100%-50%)=50% rather than (100% + 50%) = 150%
        - speed up
            - use the (old execute time) / (new execute time)
                - old time = old instruction count * old average cycle per instruction / clock rate
                - new time = new instruction count * new average cycle per instruction / clock rate
                    - old time / new time = old instruction count * old average cycle per instruction / (new instruction count * new average cycle per instruction)

            
- Could explain why “Power Wall” is a problem?
    - situation
        - can not reduce voltage further, and will make transistor more leaky

    - Power = Capacitive Load * Voltage * Frequency
    - Understand what are the challenges on multicore processors
        - Multicore processors: more than one core per chip
        - Hard to do
            - Programming for performance (not only for correctness)
            - Load balancing
            - Optimizing communication and synchronization
            
    - Fallacies and Pitfalls
        - Fallacy: Some commonly held misconceptions that you might encounter
            - Computers at low utilization use little bit power
            - Designing for performance and designing for energy efficiency are unrelated
        - PiGall: easily made mistakes
            -  They are only true in a limited context
            - Can help you avoid making the same mistakes
                - example:
                    - If you improve one aspect of a computer, then you would expect a proportional improvement in the overall performance
                    - Using a subset of the performance equal on as a performance metric.
                    - MIPS as a Performance Metric
            
    - e.g. MIPS, Amdahl’s Law, etc.
    
###chapter 2
- Understand what is instruction and instruction set?
    - instruction set: the vocabulary of all commands understood
        - different computer have different instruction set
    - instruction: words of computer's language 
    - instruction set architecture(ISA): ISA serves as the interface between software and hardware
        - provide the mechanism by which software tells hardware what should be done
- Differences between RISC and CISC
    - RISC
        - reduced instruction set computer
        - difference
            - fixed instruction lengths 32 bits
            - load store instruction sets
            - limited addressing modes
            - limited operations
            - simpler, cheaper
            - MIPS: typical of RISC ISAs
    - CISC
        - x86
- MIPS ISA
    - MIPS has a number 32 32-bit registers
        - 32 bit data called a word
        - memory is byte addressed
            - each address identifies a byte
        - MIPS is big endian
     
    - R and I types of instruction format
        - R-format
            - `op(6 bits)-rs(5 bits)-rt(5 bits)-rd(5 bits)-shamt(5 bits)-funct(6 bits)`
            - add, sub
        - I-format
            - `op(6 bits)-rs(5 bits)-rt(5 bits)-constant or offset address(16 bits)`
            - addi, lw, sw, beq, bne
    
    - Big endian, little endian
        - little endian: **least** significant byte store at least-address of memory 
        - big endian: **Most** significant byte store at least-address of memory 
    -  Memory alignment 
        - although computer are byte-addressable
        - memory typically organised in n-byte lines
        - **only the char[N] are the same in both big endian and little endian**

- How to represent unsigned and signed integers
    - What is 2s-complement, how, why
        - Most-negative: 1000 0000 ... 0000
        - Most-positive: 0111 1111 ... 1111
        - Bit 31 is called “sign bit”
        - 求负：取反加一
    
-  Sign extension
    - leading bit = 1 -> negative
    - range
        - –2,147,483,648t o +2,147,483,647
    - Sign extension: replicate the sign bit to the left  
    - 2^31 - 1 = 0x7FFFFFFF
    - -2^31 = 0x80000000
    - overflow problem
        - for add instruciton
            - 128 + x > 2^31 - 1 the upper bound
            - 128 + x < -2^31 the lower bound
        - so if you want to overflow, you need to bigger than 2^31 - 1 and smaller than -2^31 
-  Logical operations: sll, srl, and, or, nor

-  Conditional operations: beq, bne   
    - beq: branch equal
    - bne: branch not equal
 
- Concept of “basic block”
    - a basic block is a sequence of instructions with no embedded branch, no branch target

- How “Procedure calling” is supported
    - procedure is used to structure program
    - each procedure performs a specific task
    - working like a black box
    
- Know jal (for calling), and jr (for return)
    - jal procedureName
        - puts address of following instruction in $ra
        - jump to target address
        - procedure call
    - jr $ra
        - jump-register
        - copy $ra to PC
        - procedure return 

-  Understand the fact(n) assembly example

-  The memory layout of a program
-  J-type instruction format, e.g., j and jal
    - `op(6 bits)-instruction address(26 bits)`
    
-  Know how to calculate the target of PC-relative addressing, and target of (pseudo) direct jump addressing
    - target address = PC + offset * 4
    - pseudo instructions: not real instruction
        - move $t0, $t1 -> add $t0, $zero, $t1
        - blt $t0, $t1, L -> slt $at, $t0, $t1
             - bne $at, $zero, L
        - $at : assembler temporary 
    
- Hardware synchronisation instructions
    - ll rt, offset(rs)
        - load linked
  
    - sc rt, offset(rs)
        - store conditional
    - rt is both input and output
-  Know what information is stored in object modules
    - the assembler translate program into **machine instructions** which are stored in object modules

-  Know what are Compiler, Assembler, Linker, Loader used for?
    - C program compile through compiler
    - the compiler come up with assembly language program
    - then assembler generate object(Machine language module)
    - object(machine language module and library routine) go to linker
    - the linker static link and generate executable machine language program
    - then go to loader and load into memory

-  A few fallacies and pithalls
    - instruction count and CPI are not good performance indicators in isolation
    - compiler optimisation are sensitive to algorithm
    - java compiled code s significantly faster than JVM interpreted
    - nothing can fix a dumb algorithm
    - use assembly code for high performance
    - powerful instruction -> high performance
    - importance of binary compatibility => instruction set does not change
    - sequential words are at sequential byte addresses
        - increment by 4
    - using a pointer to an automatic variable outside its defining procedure
        - e.g passing pointer back via returning result
            - because pointer becomes invalid when stack popped

- MIPS instruction

- MIPS instructions | Name | format
------|-------|-------
add|add|R
subtract|sub|R
add immediate|addi|I
load word|lw|I
store word | sw | I
load half | lh | I
load half unsigned | lhu | I
store half | sh | I
load byte | lb |  I 
load byte unsigned| lbu | I
store byte | sb | I
load linked | ll | I
store conditional | sc | I
load upper immediate | lui | I
and | and | R
or | or | R
nor | nor | R
and immediate | andi | I
or immediate | ori | I
shift left logical | all | R
shift right logical | srl | R
branch on equal | beq | I
branch on not equal | bne | I
set less than | slt | R
set less than immediate  | slti | I
set less than immediate unsigned| sltiu | I
jump | j | J
jump register | jr | R
jump and link | jal | J

- thus we can see that R instruction contain the kind
    - add, sub, and, or , nor, slt, shift, jump register, move, multi
- the I instruction contain 
    - contain the load, store, immediate command, branch
- J instruction only have j and jal

- 汇编代码示例
    - 1.`if (i == j) f = g + h; else f = g - h`
        - beq $s3, $s4, Then
        - sub $s0, $s1, $s2
        - J Exit
        - Then: add $s0, $s1, $s2
        - Exit: ...
    - 2.`while(array[i] == k) i+=1`
        - Loop:sll $t1, $s3, 2 //t1 = i * 4
        - add $t1, $t1, $s6
        - lw $t0, $t1
        - beq $s5, $t0, EXIT
        - addi $s3, $s3, 1
        - j Loop
        - EXIT:...
    - 3.leaf procedure example
        - ```
        int leaf_example(int, g, h, i, j){
            int f;
            f = (g + h) - (i - j);
            return f;
        }
       ```
        
        - MIPS code:
            
            - addi $sp, $sp, -4  //save s0 on stack
            - sw $s0, 0($sp)
            - add $t0, $a0, $a1
            - add $t1, $a2, $a3
            - sub $s0, $t0, $t1
            - add $v0, $s0, $zero   //store result
            - lw $s0, 0($sp)   //store s0
            - addi $sp, $sp, 4
            - jr $ra  //return
            
            
     - 4.no leaf procedure example
         - ```
         int fact(int n){
             if(n < 1){
                 return 1;
             }else{
                 return n * fact(n - 1);
             }
         }
         int main(){
             int n = 10;
             fact(n);
             printf(n);
         }
         ```
         
         - MIPS code:
             
             - fact:
                - addi $sp, $sp, -8
                - lw $ra, 4($sp)
                - lw $a0, 0($sp)
                - slti $t0, $a0, 1  //n < 1, t0 = 1
                - beq $t0, $zero, L1 //if t0 == 0(means n >= 1) go to L1
                - addi $v0, $zer0, 1
                - addi $sp, $sp, 8
                - jr $ra //return address                
             - L1:
                - addi $a0, $a0, -1 //n = n - 1
                - jal fact //递归
                - sw $a0, 0($sp)
                - sw $ra, 4($sp)
                - addi $sp, $sp, 8
                - multi $v0, $a0, $v0 //n*fact(n-1)
                - jr $ra  //return address
             

- segment place
    - code segment -> data segment -> heap segment -> stack segment
###chapter 3
-  Given a logic function, know how to draw its logic gate diagram
    
-  Given a logic gate diagram, know how to write down its logic function
-  Know how a full adder is implemented
-  Know what are decoder and multiplexer and how they work
-  Understand clock, register, SRAM, DRAM
    - SRAM:static Random Access Memory
    - DRAM:dynamic Random Access Memory
    
    