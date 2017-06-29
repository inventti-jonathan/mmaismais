# Maquina++

A microcontroller implementation on Logisim, useful for didactic purposes.

![Print](https://cloud.githubusercontent.com/assets/13054871/26154729/089bc78e-3ae7-11e7-92ec-bc1c25bc1341.png)

### What is it?
Maquina++ (<i>Machine++</i>) is a FURB University's project released in 2003. It was initially created by Jonathan Manoel Borges, who created the entire microcontroller and his assembler, with orientation of professor Miguel Alexandre Wisintainer. This was the first version of the project that is used untill now as an academic tool.
In 2014 it was rewritten and improved on the Logisim digital simulator.
In 2017 it was rewritten again on the Logisim digital simulator, with didactics improved.

### Caracteristics
* 8-bit RAM bus
* 8-bit Data bus
* 16-bit ROM bus
* 4 input bus
* 4 output bus
* 10 ULA operations instruction set (logic and arithmetic)
* 5 jump operations
* Assembly-like language
* EOI flag
* Carry flag
* Zero flag
* 4 8-bit registers (B-E) + 8-bit Accumulator(A)

### 15 operations, 8 bits? 
In the initial project, there was 3 bits that identify the ALU operation code. The controller module gained one extra bit to address the instruction register, so we could use 15 positions. This bit is set with a special instruction called High Decoder, this instruction is generated by the assembler and the assembly programmer don't need to care about that.
With the rewrite and improvement in 2014 was added a counter with 5 bits to the controller, then we could use all the instruction register positions.
The HD counter is incremented with successive calls to High decoder operation, it acts like a page marker, if i want a instruction that is on the 3rd page, i say "turn the page 3 times", then i say, "use the 2nd instruction on this page" for example.

### How to write instructions?
In binary, the bits of the instructions are separated like
<table width="30%">
  <tr>
    <td width="33.33%" align="center"><b>ALU Operation</b></td>
    <td width="33.33%" align="center"><b>Register / I\O Port</b></td>
    <td width="33.33%" align="center"><b>Operation Flow</b></td>
  </tr>
  <tr>
    <td width="33.33%" align="center">000</td>
    <td width="33.33%" align="center">00</td>
    <td width="33.33%" align="center">000</td>
  </tr>
</table>

### Intruction set
<table width="50%">
  <tr>
    <td width="20%" align="center"><b>Code</b></td><td width="80%" align="center"><b>Name</b></td>
  </tr>
  <tr>
    <td width="20%" align="center">000</td><td width="80%" align="center">ADD</td>
  </tr>
  <tr>
    <td width="20%" align="center">001</td><td width="80%" align="center">SUB</td>
  </tr>
  <tr>
    <td width="20%" align="center">010</td><td width="80%" align="center">AND</td>
  </tr>
  <tr>
    <td width="20%" align="center">011</td><td width="80%" align="center">OR</td>
  </tr>
  <tr>
    <td width="20%" align="center">100</td><td width="80%" align="center">XOR</td>
  </tr>
  <tr>
    <td width="20%" align="center">101</td><td width="80%" align="center">NOT</td>
  </tr>
  <tr>
    <td width="20%" align="center">110</td><td width="80%" align="center">MOV</td>
  </tr>
  <tr>
    <td width="20%" align="center">111</td><td width="80%" align="center">INC</td>
  </tr>
</table>

### Operation flow table
<table width="50%">
  <tr>
    <td width="20%" align="center"><b>Code page</b></td><td width="10%" align="center"><b>Code</b></td><td width="70%" align="center"><b>Name</b></td>
  </tr>
  <tr>
    <td width="20%" align="center">00000</td><td width="10%" align="center">000</td><td width="70%" align="center">A -> A</td>
  </tr>
  <tr>
    <td width="20%" align="center">00000</td><td width="10%" align="center">001</td><td width="70%" align="center">A -> Register</td>
  </tr>
  <tr>
    <td width="20%" align="center">00000</td><td width="10%" align="center">010</td><td width="70%" align="center">A -> RAM</td>
  </tr>
  <tr>
    <td width="20%" align="center">00000</td><td width="10%" align="center">011</td><td width="70%" align="center">A -> OUT</td>
  </tr>
  <tr>
    <td width="20%" align="center">00000</td><td width="10%" align="center">100</td><td width="70%" align="center">Register -> A</td>
  </tr>
  <tr>
    <td width="20%" align="center">00000</td><td width="10%" align="center">101</td><td width="70%" align="center">RAM -> A</td>
  </tr>
  <tr>
    <td width="20%" align="center">00000</td><td width="10%" align="center">110</td><td width="70%" align="center">IN -> A</td>
  </tr>
  <tr>
    <td width="20%" align="center">00000</td><td width="10%" align="center">111</td><td width="70%" align="center">High decoder</td>
  </tr>
  <tr>
    <td width="20%" align="center">00001</td><td width="10%" align="center">000</td><td width="70%" align="center">ROM -> A</td>
  </tr>
  <tr>
    <td width="20%" align="center">00001</td><td width="10%" align="center">001</td><td width="70%" align="center">ROM -> Register</td>
  </tr>
  <tr>
    <td width="20%" align="center">00001</td><td width="10%" align="center">010</td><td width="70%" align="center">ROM -> RAM</td>
  </tr>
  <tr>
    <td width="20%" align="center">00001</td><td width="10%" align="center">011</td><td width="70%" align="center">JMP</td>
  </tr>
  <tr>
    <td width="20%" align="center">00001</td><td width="10%" align="center">100</td><td width="70%" align="center">JMPC</td>
  </tr>
  <tr>
    <td width="20%" align="center">00001</td><td width="10%" align="center">101</td><td width="70%" align="center">JMPZ</td>
  </tr>
  <tr>
    <td width="20%" align="center">00001</td><td width="10%" align="center">110</td><td width="70%" align="center">CALL</td>
  </tr>
  <tr>
    <td width="20%" align="center">00010</td><td width="10%" align="center">000</td><td width="70%" align="center">RET</td>
  </tr>
  <tr>
    <td width="20%" align="center">00010</td><td width="10%" align="center">001</td><td width="70%" align="center">DRAM -> A</td>
  </tr>
  <tr>
    <td width="20%" align="center">00010</td><td width="10%" align="center">010</td><td width="70%" align="center">A -> DRAM</td>
  </tr>
  <tr>
    <td width="20%" align="center">00010</td><td width="10%" align="center">011</td><td width="70%" align="center">PUSH</td>
  </tr>
  <tr>
    <td width="20%" align="center">00010</td><td width="10%" align="center">100</td><td width="70%" align="center">POP</td>
  </tr>
  <tr>
    <td width="20%" align="center">00010</td><td width="10%" align="center">101</td><td width="70%" align="center">PUSHA</td>
  </tr>
  <tr>
    <td width="20%" align="center">00010</td><td width="10%" align="center">110</td><td width="70%" align="center">POPA</td>
  </tr>
</table>
<sup>* All the instruction with code 111 in all code pages are High decoder instructions</sup>

### Registers's addresses
<table width="50%">
  <tr>
    <td width="20%" align="center"><b>Code</b></td><td width="80%" align="center"><b>Name</b></td>
  </tr>
  <tr>
    <td width="20%" align="center">00</td><td width="80%" align="center">B</td>
  </tr>
  <tr>
    <td width="20%" align="center">01</td><td width="80%" align="center">C</td>
  </tr>
  <tr>
    <td width="20%" align="center">10</td><td width="80%" align="center">D</td>
  </tr>
  <tr>
    <td width="20%" align="center">11</td><td width="80%" align="center">E</td>
  </tr>
</table>


### Oh, I prefer to write code in assembly language...
### No problem!
The `Assembler.jar` file is a Java assembler that compiles source to the Logisim's memory map format, so you can write code and import it to simulation. Some basic examples:

**Print hexa 44 on OUT1**

    loop:
        MOV 44,A;
        MOV A,OUT1;
    JMP loop;

**SUM hexa 55 and hexa 66**

    loop:
        MOV 55,A;
        MOV 66,B;
        ADD B,A;
        MOV A,OUT1;
    JMP loop;
    
**Function calls**

    loop:
        MOV 55,A;
        MOV 66,B;
        CALL SUM;
        JMP LOOP;
        SUM:
            ADD A,B;
            RET;
    JMP loop;
            
**MOV flows**

    MOV 11,B;
    MOV 11,C;
    MOV 11,D;
    MOV 11,E;
    MOV B,A;
    MOV C,A;
    MOV D,A;
    MOV E,A;
    MOV A,OUT1;
    MOV E,A
    MOV A,OUT2;
    loop:
    JMP LOOP;
    
**Multiple lables**

    INICIO:
        JMP LOOPA;
        MOV 11,B;
        MOV 11,B;
    LOOPA:
        JMP LOOPB;
        MOV 11,B;
        MOV 11,B;
    LOOPB:
        JMP LOOPC;
        MOV 11,B;
        MOV 11,B;
    LOOPC:
        JMP INICIO;

**RAM access**

    MOV 33,A;
    MOV A,#00;
    MOV #00,A;
    MOV A,OUT1;
    
**Turn on off**

    MOV IN0,A;
    AND 32,A;
    JMPZ OFF;
    ON:
        MOV 01,A;
        MOV A,OUT1;
        JMP END;
    OFF:
        MOV 00,A;
        MOV A,OUT1;
    END:
        JMP END;

**Dynamic memory access - Sets hex 01 to first 10 addresses of the RAM**

    MOV 00,B;
    LOOP:
        MOV 01,A;
        MOV A,#B;
        MOV B,A;
        INC A,A;
        MOV A,B;
        SUB 0A,B;
        JMPZ EXIT;
        MOV A,B;
    JMP LOOP;
    EXIT:
        JMP EXIT;
