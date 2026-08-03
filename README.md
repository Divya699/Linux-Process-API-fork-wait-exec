<img width="1386" height="805" alt="image" src="https://github.com/user-attachments/assets/7ddd901f-f96b-4564-a14c-fd263ee5290a" /># Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.



### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls


#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main()
{
    pid_t pid;

    pid = fork();

    if (pid < 0)
    {
        printf("Fork failed!\n");
        exit(1);
    }
    else if (pid == 0)
    {
        printf("\n----- Child Process -----\n");
        printf("Child PID  : %d\n", getpid());
        printf("Parent PID : %d\n", getppid());
        sleep(2);
    }
    else
    {
        printf("\n----- Parent Process -----\n");
        printf("Parent PID : %d\n", getpid());
        printf("Child PID  : %d\n", pid);

        wait(NULL);

        printf("Child process completed.\n");
    }

    return 0;
}

##OUTPUT

<img width="436" height="478" alt="image" src="https://github.com/user-attachments/assets/bf948473-b665-4c62-810f-5342081670f3" />




## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main()
{
    int status;

    printf("Running ps using execl()\n");

    if (fork() == 0)
    {
        execl("/bin/ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }

    wait(&status);

    if (WIFEXITED(status))
        printf("Child exited with status = %d\n", WEXITSTATUS(status));

    printf("\nRunning ps using execlp()\n");

    if (fork() == 0)
    {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }

    wait(&status);

    if (WIFEXITED(status))
        printf("Child exited with status = %d\n", WEXITSTATUS(status));

    printf("\nProgram completed successfully.\n");

    return 0;
}


##OUTPUT


<img width="1386" height="805" alt="image" src="https://github.com/user-attachments/assets/72db2079-94a5-4f70-9bf4-dbcf270992e2" />
















# RESULT:
The programs are executed successfully.
