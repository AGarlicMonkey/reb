# reb

**reb** is a commandline tool designed to work with CMake that embeds resources into C/CPP executables.

## Usage

**reb** takes a file and dumps it's contents into a c-style array, allowing it to be accessed in C/C++ source code.  
It takes 3 inputs: output file name (without file type), input resource file and `fopen` [mode](https://en.cppreference.com/w/c/io/fopen)  

To use this in CMake you can make a custom command:
```
add_subidrectory(reb)

set(output MyOutputFile)
set(resource /absolute/path/to/MyBinaryOrTextResourceFile.jpg)

add_custom_command(
    OUTPUT ${output}.c
	COMMAND reb ${output} ${resource} "rb"
	DEPENDS ${resource}
)

add_executable(MyExe ${output}.c)
```
(It is recommened to use `rb` for binary files and `r` for text files.)

This will generate a C file called `myoutputfile.c` with the following definitions:
```C
const unsigned char myoutputfile[] = {
	//File contents as hex
};
const size_t myoutputfileLength = sizeof(myoutputfile);
```

You can then reference in your executable:
```C
extern const unsigned char myoutputfile[];
extern const size_t myoutputfileLength;
```
