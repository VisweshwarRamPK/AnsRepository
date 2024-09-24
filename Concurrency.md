**10)CONCURRENCY:**

**I) DEFINITION:**

**Concurrency in Java refers to the ability of the program to execute multiple tasks simultaneously.It is like doing multiple tasks at the same time, but not necessarily all at once. Think of it as switching between tasks quickly, so each one seems to be happening together. In Java, we use threads to handle this. A thread is a small unit of a program that can run independently.**

**For example:**



* **You could have one thread downloading a file while another thread is updating the user interface.**
* **Even if they don’t run exactly at the same moment, Java lets them make progress by switching between them fast.**

**This makes the program more efficient, especially when there are multiple things to do at once.**

**II) JAVA THREADS:**

**Thread:**

**Thread class: You can extend the <code>Thread</code> class to create a new thread.</strong>

**CODE:**

**class MyThread extends Thread {**

**    public void run() {**

**        System.out.println("Thread is running...");**

**    }**

**}**

**MyThread t = new MyThread();**

**t.start(); // starts the thread**

**Runnable:**

**Runnable interface: You can implement the <code>Runnable</code> interface and pass it to a <code>Thread</code> object.</strong>

**class MyRunnable implements Runnable {**

**    public void run() {**

**        System.out.println("Runnable is running...");**

**    }**

**}**

**Thread t = new Thread(new MyRunnable());**

**t.start(); // starts the thread**

**III) THREAD LIFECYCLE:**

**A thread can be in one of the following states. Use Thread.getState() to get the current state of the thread.**

**NEW: created the thread but has not started execution.**

**RUNNABLE: started execution.**

**Blocked: The thread is waiting for a resource to be available or some condition to be met.**

**Waiting: waiting for some other thread to perform a task.**

**Terminated: The thread has completed its execution.**

**IV) CONCURRENCY CHALLENGES:**

**Race conditions: Multiple threads accessing shared resources can lead to unpredictable results if not synchronized properly.**

**Deadlocks: Two or more threads are waiting on each other, causing all of them to be stuck.**

**V) SYNCHRONIZATION:**

**Synchronization ensures that only one thread can access the resource at the given point of time,which prevents race conditions.**

**Synchronized block:**

**synchronized(this) {**

**    // critical section**

**}**

**Synchronized method:**

**public synchronized void methodName() {**

**    // critical section**

**}**

**VI) EXECUTORS AND THREAD POOLS:**

**Java provides the Executor framework to manage a pool of threads rather than creating and managing threads again and again can be expensive in terms of system resources.**

**Thread pools allow for reuse of threads, which improves efficiency by reducing the overhead of creating and destroying threads repeatedly.**

**CODE:**

**ExecutorService executor = Executors.newFixedThreadPool(5);**

**executor.submit(new MyRunnable());**

**executor.shutdown();**

**DEFINITION:**

**ExecutorService and Executors.newFixedThreadPool(5): **ExecutorService is an interface in Java's `java.util.concurrent` package that provides a framework for managing a pool of threads, making it easier to execute tasks 

**newFixedThreadPool(5): **creates a pool of 5 threads. The number "5" means that at most 5 threads will be active at a time. When a task is submitted, it will be executed by one of the available threads in the pool. If all threads are busy, the task will wait in the queue until a thread becomes available.

**executor.submit(new MyRunnable()) : This line submits a task (an instance of <code>MyRunnable</code>, which is a class that implements the <code>Runnable</code> interface) to the executor.</strong>

**Runnable: A <code>Runnable</code> is a functional interface with a <code>run()</code> method that represents a task. When this task is submitted, one of the threads from the pool will pick it up and execute the <code>run()</code> method of <code>MyRunnable</code>.</strong>

**Submit: The <code>submit()</code> method allows you to submit a task to the executor for execution. The executor handles scheduling the task for execution by a thread in the pool.</strong>

**executor.shutdown(): After submitting tasks, it's important to shutdown the executor, which tells the executor service that no more tasks will be submitted. Once all the tasks have finished executing, the executor service will shut down.**



* **It ensures that the application does not keep running indefinitely. The executor service will wait for all threads to complete their current tasks before shutting down.**

**If you don't call <code>shutdown()</code>, the program may continue running because the executor keeps the application alive by waiting for more tasks.</strong>

**VII)HOW TO AVOID DEADLOCK:**

**A deadlock happens when two or more threads are waiting for each other to release resources, and as a result, none of the threads can continue.**

** \
CODE FOR DEADLOCK:**

import java.util.concurrent.locks.ReentrantLock;

public class Main {

    public static void main(String[] args) {

        ReentrantLock lockA = new ReentrantLock();

        ReentrantLock lockB = new ReentrantLock();

        Thread threadA = new Thread(() -> {

            lockA.lock();

            try {

                System.out.println("Thread-A has acquired Lock-A");

                lockB.lock();

                try {

                    System.out.println("Thread-A has acquired Lock-B");

                } finally {

                    lockB.unlock();

                }

            } finally {

                lockA.unlock();

            }

        });

        Thread threadB = new Thread(() -> {

            lockB.lock();

            try {

                System.out.println("Thread-B has acquired Lock-B");

                lockA.lock();

                try {

                    System.out.println("Thread-B has acquired Lock-A");

                } finally {

                    lockA.unlock();

                }

            } finally {

                lockB.unlock();

            }

        });

        

        threadA.start();

        threadB.start();

    }

}

**Here, ThreadA acquires lockA and is waiting to lockB. ThreadB has acquired lockB and is waiting to acquire lockA. Here, threadA will never acquire lockB as it is held by threadB. Similarly, threadB can never acquire lockA as it is held by threadA. This kind of situation is called a deadlock.**

**TO AVOID DEADLOCK:**

**import java.util.concurrent.locks.ReentrantLock;**

**public class Main {**

**    public static void main(String[] args) {**

**        ReentrantLock lockA = new ReentrantLock();**

**        ReentrantLock lockB = new ReentrantLock();**

**        Thread threadA = new Thread(() -> {**

**            synchronizedLocks(lockA, lockB);**

**        });**

**        Thread threadB = new Thread(() -> {**

**            synchronizedLocks(lockA, lockB);**

**        });**

**        threadA.start();**

**        threadB.start();**

**    }**

**    private static void synchronizedLocks(ReentrantLock lock1, ReentrantLock lock2) {**

**        lock1.lock();**

**        try {**

**            System.out.println(Thread.currentThread().getName() + " has acquired Lock 1");**

**            lock2.lock();**

**            try {**

**                System.out.println(Thread.currentThread().getName() + " has acquired Lock 2");**

**                // Critical section here**

**            } finally {**

**                lock2.unlock();**

**            }**

**        } finally {**

**            lock1.unlock();**

**        }**

**    }**

**}**

**Locking lock1: The first lock (<code>lock1</code>) is acquired using <code>lock1.lock()</code>. If it is not available, the thread will wait until it can acquire it.</strong>

**Locking lock2: The thread then attempts to acquire the second lock (<code>lock2</code>). This is done inside a <code>try</code> block to ensure that if <code>lock2</code> is acquired, it can be unlocked later.</strong>



* **Define a strict order in which resources should be acquired. All threads must follow the same order when requesting resources.**
* **Use tryLock: The <code>Lock</code> interface's <code>tryLock()</code> method allows you to attempt acquiring a lock without waiting indefinitely, helping avoid deadlocks.</strong>
* <strong>Avoid nesting of locks. The cause for the deadlock in the previous example was that the threads were not able to release one lock without acquiring the other lock.</strong>
* <strong>Ensure that threads do not acquire multiple resources simultaneously. If a thread holds one resource and needs another, it should release the first resource before attempting to acquire the second</strong>
* <strong>Set timeout for threads If a thread cannot acquire a lock within a specified time, it releases all acquired locks and tries again later. This prevents a situation where a thread holds a lock indefinitely, potentially causing a deadlock.</strong>

<strong>VIII) LOCK:</strong>

**A lock ensures that a specific task is executed by only one thread at a time, preventing conflicts when multiple threads try to access shared resources. Here's how it works:**



* **A thread tries to acquire the lock before performing a task.**
* **If successful, the thread runs the task and releases the lock once done.**

**The ReentrantLock class in Java provides methods like:**



* **<code>lock()</code>: Acquires the lock.</strong>
* <strong><code>unlock()</code>: Releases the lock.</strong>
* <strong><code>tryLock()</code>: Attempts to acquire the lock without waiting.</strong>

<strong>CODE:</strong>

**public class LockExample {**

**    private final ReentrantLock lock = new ReentrantLock();**

**    private int count = 0;**

**    public int increment() {**

**        lock.lock();**

**        try {**

**            return this.count++;**

**        } finally {**

**            lock.unlock();**

**        }**

**    }**

**}**

**In this example, the <code>lock()</code> method ensures that only one thread can increment the <code>count</code> variable at a time.</strong>

**IX) RACE CONDITION:**

**Multiple threads accessing shared resources can lead to unpredictable results if not synchronized properly. If threads access and modify shared data without proper synchronization, unexpected results can happen.**

**CODE:**

public class Increment {

    private int count = 0;

    public void increment() {

        count += 1;

    }

    public int getCount() {

        return this.count;

    }

}

public class RaceConditionsExample {

    public static void main(String[] args) {

        Increment eg = new Increment();

        for (int i = 0; i &lt; 1000; i++) {

            Thread thread = new Thread(eg::increment);

            thread.start();

        }

        System.out.println(eg.getCount());

    }

}

**When 1000 threads try to increment <code>count</code>, the final value may be less than 1000 due to a race condition. This happens because threads read and update the <code>count</code> variable simultaneously.</strong>


### **Scenario:**



* **Thread-x and Thread-y both read <code>count</code> (0), increment it, and write back 1.</strong>
* <strong>Instead of the expected 2, the final value remains 1, as both threads overwrote each other’s updates.</strong>

<strong>This happens because there’s no synchronization, and threads are racing to modify the value. Proper synchronization (e.g., using locks) is required to avoid this issue.</strong>

**Solving this issue by lock:**

**To solve the race condition issue, you can use a lock to ensure that only one thread can modify the <code>count</code> variable at a time. This prevents multiple threads from simultaneously reading and updating the shared resource, avoiding the problem.</strong>

**CODE:**

**import java.util.concurrent.locks.ReentrantLock;**

**public class Increment {**

**    private int count = 0;**

**    private final ReentrantLock lock = new ReentrantLock();**

**    public void increment() {**

**        lock.lock(); // Acquire the lock**

**        try {**

**            count += 1;**

**        } finally {**

**            lock.unlock(); // Release the lock**

**        }**

**    }**

**    public int getCount() {**

**        return this.count;**

**    }**

**}**

**public class RaceConditionsExample {**

**    public static void main(String[] args) throws InterruptedException {**

**        Increment eg = new Increment();**

**        // Create 1000 threads to increment count**

**        for (int i = 0; i &lt; 1000; i++) {**

**            Thread thread = new Thread(eg::increment);**

**            thread.start();**

** **

**        }**

**        // Print the final count value**

**        System.out.println(eg.getCount());**

**    }**

**}**