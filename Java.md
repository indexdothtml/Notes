# Java Notes

## How Java works executes the code under the hood.

First you write the code in Java language, which human can understand because of english wordings.

You as a developer create a Java file and write a code inside it. (Java file will have .java extension)
ex - `Hello.java`

Next step, you compile this .java or if there are multiple files then all files. You can compile the files by calling compiler using `javac` command.
ex - `javac Hello.java` or `javac Hello.java anotherFile.java oneMoreFile.java`

After compilation command executes, either you will get error message, if there is any error in java code, or compilation will successful and generate Byte code.

If Java file have any error, then after executing compilation command, java compiler will give error message and hint to solve the error.

If Java file does not have any error, then after executing compilation command, java compiler generate Byte code, that can be used to execute our program which machine can understand.

Now, Byte code is written inside special file which will have an extension called .class, so after successful compilation, compiler generates .class file ex- `Hello.class` this file contains Byte code, that can understandable by machine and it executes.

Now, Java is platfrom independent, that means whatever the OS your machine is running, java code can execute on that machine.

So, executing code on different platfrom is not that easy because different OS has different architecture, so it needs something on top of that who can do this job of executing the java program.

To run java programs on different platfrom, we need someone to do that job for that perticular platfrom, becuase platfrom itself can't do that, so we have JRE means Java Runtime Environment.

JRE, Java Runtime Environment, as name suggest it is a environment created on top of that platfrom so java program can run easily. So your computer/machine is hardware, on that you install OS so it is platfrom, so it is different, you can have different platfroms/OS. For each platfrom, that platfrom supporting JRE is developed and that JRE will run on OS.

Now, JRE comes with JDK, Java Development Kit which we install when we want to develop and run java applications. So JRE is the part of JDK.

Now, JRE contains JVM, Java Virtual Machine which is actually used to execute your java application.

JVM, takes your Byte code and executes it, when you write `java Hello` after your compilation, JVM takes .class file and executes it, with the help of `java` command we are calling JVM to execute the code.

Summary -

JVM is a part of JRE and JRE is a part of JDK.

JDK > JRE > JVM.

Java is platfrom independent, because java code can run on any platfrom, either windows, mac, linux, android etc.

How Java code becomes platfrom independent because, Java code gets converted into machine code or Byte code that every machine in this world can understand irrespective of its OS.

JVM can understand Byte code and executes for us. But JVM is also a one software or program that needs to run on machine, but it is not platfrom independent, Here important is JVM, JRE and JDK is not platfrom independent which used to run java code but final java code which is byte code is platfrom indepenent.

JVM needs environment where it can run so it runs on JRE and this things comes in one kit called JDK, which we install in our system.

But JVM understand Byte code only and it executes Byte code, thats why it is machine independent because every machine/system can understand byte code, but we developer can't code in Byte code.

So, we write code in Java language, and to convert the code into Byte code which JVM can understand there is compiler in mid, so compiler is a mid person who can understand java and byte code and converts java code into byte code so JVM can handle execution.

`javac` is java compiler, it also checks syntax and gives error if any language rule not followed.
