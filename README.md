# Various System Calls Implementation

## SystemCall.c

### int main(argc, char \*\*argv)
_Description_ : Takes and analyzes the command line arguments and passes the control to appropriate file type method.

_Parameters_ :
  1. argc (int) -> Number of command line arguments passed
  2. argv (char \*\*)
      - File Type (String)
        - npipe : Named pipe
        - unpipe : Unnamed Pipe
        - regular : Regular File
      - Name of the file (String)
      - Mode of operation (String)
        - create
        - read
        - write
        - status
      - Offset (int) -> Provides random access of file for read and write mode of operation
      - Whence (String) -> Specifies the position, from where to place the offset
        - current
        - start
        - end

_Return_ : 0 on completing the execution.

## NamedPipe.h

Implements the create, read, write and status functionalities for named pipe.

### void named_pipe(int argc, char \*\*argv)

_Description_ : Takes the command line arguments as input, checks for the specific number of arguments and passes the control to appropriate method to perform the specified operation, or prints the error if no valid operation specified.

_Parameters_ :
  1. argc (int) -> Number of command line arguments passed
  2. argv (char \*\*)
      - File Type (String)
        - **npipe : Named pipe**
        - unpipe : Unnamed Pipe
        - regular : Regular File
      - Name of the file (String)
      - Mode of operation (String)
        - create
        - read
        - write
        - status

_Return_ : None.

### int create_named_pipe(char \*file_name)

_Description_ : Creates the new named pipe with the name as file_name and 010777 as rwx permissions using mknod system call.

_Parameters_ :
  1. file_name (char \*) -> name of the file to be created.

_Return_ : 1 on success, else exit.


### int open_named_pipe(char \*file_name, int mode)

_Description_ : Opens the pipe named as file_name in the specified mode.

_Parameters_ :
  1. file_name (char \*) -> name of the named pipe to be opened.
  2. mode (int)
      - read
      - write

_Return_ : fd of the opened named pipe on success, else exit.

### void close_named_pipe(int fd)

_Description_ : Closes the named pipe with the file descriptor as fd (returned by open system call).

_Parameters_ :  
  1. fd (int) -> File descriptor of the opened named pipe

_Return_ : None.

### void read_named_pipe(char \*file_name)

_Description_ : Opens the named pipe in read mode using open_named_pipe method and reads the data from the named pipe using read system call, after completion of read it closes the named pipe using close_named_pipe method.  

_Parameters_ :
  1. file_name (char \*)

_Return_ : None.

### void write_named_pipe(char \*file_name)

_Description_ : Opens the named pipe in write mode using open_named_pipe method and writes the data to the named pipe using write system call, after completion of  write it closes the named pipe using close_named_pipe method.

_Parameters_ :
  1. file_name (char \*)

_Return_ : None.

### void status_named_pipe(char \*file_name)

_Description_ : Prints the status of the pipe named as file_name using the stat system call.

_Parameters_ :
  1. file_name (char \*)

_Return_ : None.

## UnnamedPipe.h

Implements the create, read, write functionalities for named pipe.

### void unnamed_pipe(int argc, char \*\*argv)

_Description_ : Takes the command line arguments as input, checks for the specific number of arguments and passes the control to unPipe method to perform operation over unnamed pipe.

_Parameters_ :
  1. argc (int) -> Number of command line arguments passed
  2. argv (char \*\*)
      - File Type (String)
        - npipe : Named pipe
        - **unpipe : Unnamed Pipe**
        - regular : Regular File
      - Name of the file (String)

_Return_ : None.

### void unPipe(char \*file_name)

_Description_ : Creates a unnamed pipe using pipe system call and performs read and write operations over unnamed pipe using read and write system call respectively, after completion it closes the unnamed pipe using close system call.

_Parameters_ :
  1. file_name (char \*) -> name of the pipe, here it is equivalent to type of file.

_Return_ : None.

## RegularFile.h

Implements the create, read, write and status functionalities for reguar files.

### void regular_file(int argc, char \*\*argv)

_Description_ : Takes the command line arguments as input, checks for the specific number of arguments and passes the control to appropriate method to perform the specified operation, or prints the error if no valid operation specified.

_Parameters_ :
  1. argc (int) -> Number of command line arguments passed
  2. argv (char \*\*)
      - File Type (String)
        - npipe : Named pipe
        - unpipe : Unnamed Pipe
        - **regular : Regular File**
      - Name of the file (String) 
      - Mode of operation (String)
        - create
        - read
        - write
        - status
      - Offset (int) -> Provides random access of file for read and write mode of operation
      - Whence (String) -> Specifies the position of where to place the offset
        - current
        - start
        - end

_Return_ : None.

### int create_regular_file(char \*file_name)

_Description_ : Creates the new regular file with the name as file_name and 00777 as rwx permissions using creat system call.

_Parameters_ :
  1. file_name (char \*) -> name of the regular file to be created.

_Return_ : 1 on success, else exit.


### int open_regular_file(char \*file_name, int oflag)

_Description_ : Opens the regular file named as file_name in the specified mode.

_Parameters_ :
  1. file_name (char \*) -> name of the regular file to be opened.
  2. oflag (int)
      - read
      - write

_Return_ : fd of the opened regular file on success, else exit.

### void close_regular_file(int fd)

_Description_ : Closes the regular file with the file descriptor as fd (returned by open system call).

_Parameters_ :  
  1. fd (int) -> File descriptor of the opened regular file
_Return_ : None.

### int lseek_random_file(int fd, int offset, char \*whence)

_Description_ : Places the read and write pointer as a specific position in the regular file with the help of offset and whence using lseek system call.

_Parameters_ :
  1. fd (int) -> File descriptor of the opened regular file
  2. offset (int) -> Position from where to start reading/writing from a regular file
  3. whence (char \*) -> Specifies the position of where to place the offset.
      - current : SEEK_CUR
      - start : SEEK_SET
      - end : SEEK_END

_Return_ : 0 on Success, -1 on Failure.

### void read_regular_file(char \*file_name, int offset, char \*whence)

_Description_ : Opens the regular file in read mode using open_regular_file method, also provides option for random read from the file using lseek_regular_file method and reads the data from the file accordingly using read system call, after completion of read it closes the regular file using close_regular_file method.  

_Parameters_ :
  1. file_name (char \*)
  2. offset (int) -> Position from where to start reading from a regular file
  3. whence (char \*) -> Specifies the position of where to place the offset
        - current
        - start
        - end

_Return_ : None.

### void write_regular_file(char \*file_name, int offset, char \*whence)

_Description_ : Opens the regular file in write mode using open_regular_file method, also provides option for random write to the file using lseek_regular_file method and writes data to the file accordingly using write system call, after completion of write it closes the regular file using close_regular_file method.  

_Parameters_ :
  1. file_name (char \*)
  2. offset (int) -> Position from where to start writing to a regular file
  3. whence (char \*) -> Specifies the position of where to place the offset
    - current
    - start
    - end

_Return_ : None.

### void status_regular_file(char \*file_name)

_Description_ : Prints the status of the regular file with name file_name using the stat system call.

_Parameters_ :
  1. file_name (char \*)

_Return_ : None.
