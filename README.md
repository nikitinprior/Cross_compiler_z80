# Cross compiler Hi-Tech C v3.09

The Hi-Tech C compiler was originally written in C by HI-TECH SOFTWARE. It is most likely that the first versions of the compiler were written in C in the style of Kernighan and Ritchie. The restored source code uses function prototypes.

The restored C compiler source code is obtained by recreating the Hi-Tech C v3.09 compiler for CP/M from binary executables.

Although HI-TECH SOFTWARE subsequently continued to develop its compiler, the C source code was recovered from the CP/M version 3.09 compiler executables. The choice was based on the merits of this version of the compiler - almost complete support for the ANSI C standard and compactness, that is, the relatively small size of executable files and, due to this, the ability of the compiler to work directly on 8-bit computers with a Z80 processor.

To check the correctness of generating executable files, the restored C source code was compiled using the Hi-Tech C compiler version 3.09 for CP/M using the zxcc emulator, and the resulting executable code was compared with the binary code from native executable files.

However, some functions included in the programs of the compiler components called by the zc3.c program turned out to be quite large in size and could not be compiled using the Hi-Tech C v3.09 compiler for CP/M. OPTIM.COM for CP/M ran out of memory when running an optimization pass for these functions. It follows from this fact that HI-TECH SOFTWARE developed its compiler using a cross compiler on an operating system other than CP/M. It was possible to perform optimization of these functions without errors only after restoring the source code of the OPTIM.COM program and creating an executable file of this program for modern operating systems based on the restored code.

Unfortunately, it is impossible to compile the restored code of some components using the Hi-Tech C v3.09 compiler for CP/M or for UZI-180, since the capabilities of these compilers are limited by the amount of available RAM.

To create a compiler version for CP/M or UZI-180 from the restored code, you can use the cross-compiler version for modern Linux, MacOS or Windows operating systems, which can handle more complex program source code.

# Creating a cross compiler for Linux, MacOS or Windows

To create a cross-compiler for Linux, MacOS or Windows operating systems, you need to compile the restored code of all programs included in the compiler on these operating systems.

To do this, run the following commands in the directory with the source code of the specific program:

1. For the control program of the zc3 compiler

gcc -O2 -o zc3 zc3.c

2. For cpp_new3 preprocessor program

gcc -O2 -ocpp_new3 cpp.c cpy.c getargs.c fname.c

To create a preprocessor, it is desirable to use the source code of the Mark Ogden version, as it fixes some bugs and provides additional features.

3. For the first pass program p1x3

gcc -O2 -op1x3 cclass.c emit.c expr.c lex.c main.c op.c program.c stmt.c sym.c type.c memchk.c

The restored source code of the first pass program will be available in the repository after Mark Ogden has finished styling it.

4. For cgen3 code generation program

gcc -o xcgen3 -O3 cgen.c

5. For optim3 optimization program

gcc -O2 -o optim3 optim.c

6. For zasx3 macro assembler program

gcc -o zasx3 -O2 code.c cclass.c expr.c lex.c macro.c main.c kwd.c parse.c sym.c tlab.c emulate.c

7. For linq3 linker program

gcc -O2 -o linq3 a.c b.c c.c ds.c e.c extra.c getargs.c fname.c

Note that the executable files must be named: cpp_new3, p1x3, cgen3, optim3, zasx3, and linq3, since they are used in the source code of the zc3.c control program to execute these programs.

8. After generating executable files, they must be copied to the directory described in the PATH environment variable.

9. For the cross compiler to work properly, two more directories must be created. One for include files and one for libraries and runtime initializers.

Include files can be placed in the directory

/usr/local/HiTech/include80

Files with libraries of standard functions and run-time initialization modules can be placed in the directory

/usr/local/HiTech/lib80

To compile programs for CP/M, crtcpm.obj and libc.lib files must be present in this directory. To compile programs for the UZI-180, crtuzi.obj and libcuzi.lib files must be present in this directory.

In addition, to specify the default search paths for include files and libraries, you need to define two more variables

export INCDIR80="/usr/local/HiTech/include80/"

export LIBDIR80="/usr/local/HiTech/lib80/"

You can add them to the .bash_profile file in the user's home directory.

After creating and filling the cross-compiler directories and defining the INCDIR80, LIBDIR80 and PATH environment variables, you can compile your source programs in any current directory using the zc3 control program with the necessary options and a list of processed programs. To compile programs for CP/M, the "-CPM" option must be specified. Without this option it is possible to compile programs for the UZI-180.

In addition, the source code of two more utilities has been restored.

To compile the object file content viewer and the library maintainer, run the commands

gcc -O2 -odump3 dump3.c

gcc -O2 -olibr3 libr.c

and copy the executable files dump3 and libr3 to the directory where the cross compiler executable files are located.

From this point on, the zxcс emulation program is no longer required, although it can be used to check the operation of the cross compiler.

If desired, you can individually perform any compilation steps by executing the specific programs you need, which are usually called by the zc3 control program.

In terms of its capabilities, the cross-compiler is not inferior to the native Hi-Tech C v3.09 compiler for CP/M and allows you to develop programs in the C or Z80 assembly language on computers with modern Linux, macOS or Windows operating systems. In addition, the cross-compiler can handle more complex source code and C++-style comments.

Since the cross compiler is based on the algorithms used by the Hi-Tech C v3.09 native compiler for CP/M, it has similar problems.

The cross compiler is not the primary purpose of recreating source code. The source code has been restored from a historical point of view.

All copyrights to the restored code still belong to HI-TECH SOFTWARE.

# Acknowledgments

Thank you to HI-TECH SOFTWARE for writing the Hi-Tech C v3.09 compiler for CP/M and allowing free use of it. 

Thanks to John Elliott for writing the zxcc emulator. It was mostly used to compile the reconstructed source code. https://github.com/agn453/ZXCC 

Thanks to Hector Peraza for adapting the UZI-180 operating system to the P112 microcomputer, which made me want to restore the source code of the Hi-Tech C V3.09 compiler. UZI-180 can be obtained from the repository https://github.com/hperaza/UZI180.

I express my gratitude to all the people who participated in restoring the source code of Hi-Tech C compiler V3.09, testing its restored versions and reporting on the bugs found, especially Mark Ogden. His contribution was the greatest, greatly speeding up the recovery process and giving it an almost professional level. The experience of working with Mark has left me with indelible feelings, added to my knowledge and experience. I am very grateful to him for the opportunity to work together.

Individual thanks to Tony Nicholson for saving materials about the Hi-Tech C v3.09 compiler for CP/M https://github.com/agn453/HI-TECH-Z80-C, to Michal Tomek and Fred Weigel for providing information about detected bugs and to Ladislau Szilagyi for his contributions to improving the compiler programs and writing the new macro assembler for Hi-Tech C V3.09 https://github.com/Laci1953/Z80AS. 

I am grateful to all the unnamed people who cared enough to restore and preserve information about this wonderful compiler and the CP/M operating system.

I apologize if I forgot to mention anyone.

Andrey Nikitin 22-07-2022.

