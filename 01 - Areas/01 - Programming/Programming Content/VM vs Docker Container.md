**Virtual Machine** - is a complete OS running inside other OS with its own kernel (e.g. Windows inside Linux).

**Docker Container** - is an isolated space, managed by docker, that borrows the host's OS kernel. 
Isolated means:
- Own filesystem
- Own network
- Own processes
Those are independent of the HOST system, the only dependent thing is the kernel.

<font color="#00b050">Why docker is good:</font>
- faster boot time 
- small size (comparing to VM)
- resources are managed by docker (meaning that they are used only when needed)

---

**When working with two different OS** we need to understand that the behavior of the code can be different and we need to isolate the processes (e.g. do not copy any files from windows to linux)