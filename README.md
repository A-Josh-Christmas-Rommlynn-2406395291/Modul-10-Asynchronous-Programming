### **1.1 Understanding how it works in initial code timer**

**Screenshot**

![Screenshot 1](/assets/images/screenshot1.png)

**Explanation:**
First, program creates two objects that called Executor and Spawner. After that, program spawns a task to print before waiting on a timer. Then, program sets timer future (timer used for waiting) for two seconds. Next, program prints after waiting on a timer. The sentence that right after `spawner.spawn(...);` will not execute until timer future finished.

### **1.2 Understanding how it works in multiple spawn and removing statement: `drop(spawner)`**

**Screenshots**

![Screenshot when spawner dropped 1](/assets/images/screenshot-when-spawner-dropped-1.png)

![Screenshot when spawner dropped 2](/assets/images/screenshot-when-spawner-dropped-2.png)

![Screenshot when spawner dropped 3](/assets/images/screenshot-when-spawner-dropped-3.png)

**Explanation:**
If the program doesn't have `drop(spawner)`, then the channel will be stayed open, so executor in `ready_queue.recv()` will continuously waiting new task even though all tasks already finished. Besides that, the program will not exit from `run`. Apart from that, because every task has own timer and they runs simultaneously, the order of `done1`, `done2`, `done` not guaranteed to be same because the order of `wake` or sending task to channel depends on thread/OS schedule or when exactly timer finished. In other words, `done1`, `done2`, `done3` can appeared in different order because of independent timer. Other than that, task scheduling is not deterministic. So, it is normal: asynchronus makes task completion become unpredictable.