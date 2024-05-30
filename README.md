# 8085-Zadaca-8

За регулирање на гужва во услужна установа е проектиран
систем каде шалтерски работник со притискање на тастер ја
најавува својата расположливост, а на дисплеј чија природа
е небитна се прикажува бројот на шалтерот и бројот на
корисникот кој е на ред. Во установата има два шалтера.
Корисниците броевите ги добиваат на влез и во еден ден
нема повеќе од 255 корисника. Да се нацрта минимално
хардверско поврзување и да се напише соодветна
асемблерска програма базирана на µP 8085A. 

**Resenie:**

![Screenshot (1)](https://github.com/slavko444/8085-Zadaca-8/blob/main/Hardware%20connection.png)


```
MVI A.0 ;реден број на корисникот

 STA RDN_BR

 MVI E,255d

VRTI: MOV A,E ;јамка за 255 корисника

 ANI FFh

 JNZ VRTI ;сите интерапти се случуваат тука

 HLT ;крај на програмата

 END


 RDN_BR DS 1 ;променлива каде се чува редниот број на корисникот

;има само 4B меморија наменета за интерапт рутините (премалку), па затоа повикуваме
процедура (CALL=3B, RET=1B)

2Ch: CALL SERVIS_55 ;на адреса 2Ch, наменета за RST 5.5

 RET

34h: CALL SERVIS_65 ;на адреса 34h, наменета за RST 6.5

 RET

SERVIS_55: MVI A,1 ;на дисплеј се испишува бројот на шалтер

 OUT 01h

 LDA RDN_BR ;се вчитува редниот број на корисникот

INR A ;се зголемува за 1, се запишува во

соодветната мемориска локација и се испишува на втоориот дисплеј

 STA RDN_BR

 OUT 02h

 DCR E ;еден корисник помалку

 RET

SERVIS_65: MVI A,2d ;на дисплеј се испишува бројот на шалтер

 OUT 01h

 LDA RDN_BR ;се вчитува редниот број на корисникот

 INR A ;се зголемува за 1, се запишува во

соодветната мемориска локација и се испишува на втоориот дисплеј

 STA RDN_BR

 OUT 02h

 DCR E ;еден корисник помалку

RET

```

**Develop by:**

[Slavko Srebrenoski ](https://github.com/slavko444)




**Subject**

Microcomputer's systems



**Built With**

This project is built using the following tools:

- [e8085](https://emu8086-microprocessor-emulator.en.softonic.com/): Assembler and emulator for the Intel 8085 microprocessor.



**Getting Started**

To get a local copy up and running, follow these steps.



**Prerequisites**

In order to run this project you need:

A working computer
Connection to internet
Setup



**How to Run**

To run the program, you need an 8085 emulator or assembler. You can use emulators like DOSBox or TASM (Turbo Assembler). Here's how to run the program using e8085.exe:

1. Download and install e8085.exe from [here](https://emu8086-microprocessor-emulator.en.softonic.com/).
2. Clone this repository to your local machine.
3. Open e8085.exe and load the `Zadaca 8 code.asm` file.
4. Assemble the code by pressing the Assemble button.
5. Run the program by pressing the Run button or by pressing F10.
