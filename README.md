# Linux-File-IO-Systems-locking
Ex07-Linux File-IO Systems-locking
# AIM:
To Write a C program that illustrates files copying and locking

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## 1.To Write a C program that illustrates files copying 
```c
#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>
int main()
{
    char block[1024];
    int in, out;
    int nread;
    in = open("filecopy.c", O_RDONLY);  // Opening the source file in read mode
    out = open("file.out", O_WRONLY|O_CREAT, S_IRUSR|S_IWUSR);  // Creating output file
    while((nread = read(in,block,sizeof(block))) > 0)
        write(out,block,nread);  // Copying the content
    exit(0);
}
```






## 2.To Write a C program that illustrates files locking
```c
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/file.h>
int main (int argc, char* argv[])
{
    char* file = argv[1];
    int fd;
    struct flock lock;
    printf ("opening %s\n", file);
    fd = open (file, O_WRONLY);  // Open file for writing

    // Acquire shared lock
    if (flock(fd, LOCK_SH) == -1) {
        printf("error acquiring shared lock\n");
    } else {
        printf("Acquiring shared lock using flock\n");
    }
    getchar();

    // Upgrade to exclusive lock (non-blocking)
    if (flock(fd, LOCK_EX | LOCK_NB) == -1) {
        printf("error acquiring exclusive lock\n");
    } else {
        printf("Acquiring exclusive lock using flock\n");
    }
    getchar();

    // Release lock
    if (flock(fd, LOCK_UN) == -1) {
        printf("error unlocking\n");
    } else {
        printf("Unlocking\n");
    }
    getchar();
    close (fd);
    return 0;
}
```



## OUTPUT

<img width="1631" height="964" alt="image" src="https://github.com/user-attachments/assets/f3023cbe-b4f6-4569-8d7d-b61269d197df" />
<img width="1238" height="1271" alt="image" src="https://github.com/user-attachments/assets/e3b28c2b-e199-42b3-970a-47cab3bf3b7c" />
<img width="1254" height="1254" alt="image" src="https://github.com/user-attachments/assets/3536d6e2-feb3-4b28-8688-0c06d3d5b0fd" />






# RESULT:
The programs are executed successfully.
