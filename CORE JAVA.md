### Core Java
#### Java Basics
##### 1) What is Java?
###### Java is an object-oriented, platform-independent, multi-threaded, high-level programming language. This was developed by James Gosling in 1991.
##### 2) What is a High-level Programming language?
###### High-level languages are programming languages that are used for writing programs or software that humans and computers can understand.
##### 3) What is Portable in Java?
###### Java Supports read-one-write-anywhere approach. We can execute the Java program on every machine.
##### 4) Architecture Neutral?
###### In C, the size of a data type may vary according to architecture (32 bits or 64 bits), which doesn't exist in Java.
##### 5) What is a platform?
###### Platform is the hardware or software environment in which a piece of code is executed.
##### 6) Is the Java platform independent?
###### Java is “platform-independent” because the code written in Java can run on any operating system (Windows, macOS, Linux, etc.) without requiring any changes. This is due to its “Write Once, Run Anywhere” (portable) feature, which is made possible by the Java Virtual Machine (JVM).
##### 7) What is a JVM, JDK, JRE, JIT?
###### JVM(Java Virtual Machine) - It provides the runtime environment in which Java bytecode can be executed.
###### JDK(Java Development Kit) - It provides an environment to develop and run Java applications.
###### JRE(Java Runtime Environment) - It provides an environment just to run Java applications.
###### JIT(Just in time) - It helps the interpreter execute Java bytecode quickly.
##### 8) What is object-oriented programming?
###### object-oriented programming deals with objects which has data and functions around them. 
###### It uses a bottom-up approach where the smaller tasks are first dealt with in detail and gradually create a huge system.
###### It gives more importance to data rather than procedure.
##### 9) JVM architecture?
![JVM architecture](https://github.com/user-attachments/assets/c6313ad9-4a9e-4d40-ab6d-672de3831c0e)
###### Java compiler converts the .java file to the .class file.
###### The JVM first loads this .class file into the class loader sub-system.
###### Run time Memory area: The program is allocated memory for different data
###### The Method area: is used to store the code of the program that is currently in execution.
###### Heap: is used to store objects created in the program during run time.
###### Stack: is used to store data when calling methods.
###### PC (Program Counter) Register: contains the address of the code of the program that is in execution.
###### Native method stack: store the native method memory.
###### Execution Engine of the JVM is a special block with an interpreter and JIT.
##### 10) What is a classloader?
###### Class loader is a subsystem of the JVM that is used to load the .class file.
###### There are 3 types of classloaders in Java.
###### i. Bootstrap Classloader: It loads the rt.jar file, which contains all class files of Java Standard Edition.
###### ii. Extension Classloader: It loads the jar files located in $Java_Home/jre/lib/ext directory.
###### iii. Application classloader: It loads the class files from the classpath.
