**Screenshot**

![Figure 2 screen capture](/assets/images/screenshot1.png)

**Explanation:**
First, program creates two objects that called Executor and Spawner. After that, program spawns a task to print before waiting on a timer. Then, program sets timer future (timer used for waiting) for two seconds. Next, program prints after waiting on a timer. The sentence that right after `spawner.spawn(...);` will not execute until timer future finished.