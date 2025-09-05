##### A little more in-depth explanation (don’t need to know) 
Most programs in their code, contain variables that are static/global, these are variables that exist for the entire lifetime of a process and are pre-allocated within the BSS and Data segments of a program file.

Think of a very basic web-browser program that can only have 1 tab. When this program is executed, its process needs to have a variable that stores the current URL. We shall name this variable `url`. 
- By default `url = "https://www.google.com"`. 
- The value of `url` can change in the process’ lifetime
- The variable `url`  is needed from the start till the end of a process

`url` is an example of a static/global variable. Since `url` is needed from the start and does not need to be unassigned during the lifetime of a process, it is pre-allocated a space within the **Data** segment of the program file. 

So smth like this `url -> "https://www.google.com"` would exist inside the data segment of the program file. 

This prevents having to waste time allocating space for `url` on the stack when the process starts. Instead, since, the `url` exists in the **Data** segment of the program file, it is just copied into the Data segment of the process when it starts. immediately allowing the process to start using `url` without having to allocate it on the stack! 

So, that explains the Data segment, what about BSS?

Think of an application that stores how long it’s been opened for in seconds. This variable we will call `timeAlive` needs to exist from the creation of the process, till the end of the process. So it is also an example of a static/global variable. However, `timeAlive` has the initial value of 0.

Instead of storing smth like `timeAlive -> 00000000 00000000 00000000 00000000` within the Data segment of the program file, which wastes so much space. Within the **Header** segment, you could just specify something like `timeAlive -> 32`, this is the BSS! The BSS segment in a program file lives within the Header segment. The BSS segment simply stores all 0 initialised global variables. And when the program is executed, the BSS is read and is then allocated in physical memory space, this is the process’ BSS segment.