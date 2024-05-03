During an interview, some interviewer asked me about the differences between Java Threads performance vs. Virtual Threads. I answered that because Virtual Threads are actually light weight threads handled by JVM, they must be faster, but I was curious about the exact performance difference between these two. So, I did a simple benchmark to see the performance improvements in Virtual Threads.  

This is a very simple test, I create a very huge number of threads and virtual threads, each takes 5 seconds to finish. Then I calculate the duration of running app.

This is Java code I used for this benchmark:

```java
package info.behzadian.thread;

import java.util.concurrent.CountDownLatch;

public class Main {

  public static void main(String[] args) throws InterruptedException {
    int numThreads = 100000;
    CountDownLatch latch = new CountDownLatch(numThreads);

    long start = System.currentTimeMillis();
    for(int i =0; i < numThreads; i++) {
      startThreads(latch);
    }
    latch.await(); // wait for all threads to finish
    long end = System.currentTimeMillis();
    System.out.println("Time taken with regular threads: " + (end - start) + "ms");

    latch = new CountDownLatch(numThreads); // reset the latch
    start = System.currentTimeMillis();
    for(int i =0; i < numThreads; i++) {
      startVirtualThreads(latch);
    }
    latch.await(); // wait for all virtual threads to finish
    end = System.currentTimeMillis();
    System.out.println("Time taken with virtual threads: " + (end - start) + "ms");
  }

  private static void startThreads(CountDownLatch latch) {
    new Thread(new Runnable() {
      @Override
      public void run() {
        try {
          Thread.sleep(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
          latch.countDown(); // decrement the count of the latch
        }
      }
    }).start();
  }

  private static void startVirtualThreads(CountDownLatch latch) {
    Thread.startVirtualThread(new Runnable() {
      @Override
      public void run() {
        try {
          Thread.sleep(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
          latch.countDown(); // decrement the count of the latch
        }
      }
    });
  }

}
```

In first run, I started with 100,000 threads vs. virtual threads and this is the result:

```
Time taken with regular threads: 54639ms
Time taken with virtual threads: 9477ms
```

As you can see, virtual threads are much faster. They take around 17% running time of threads.

Then, I tried with 200,000 threads benchmark and this is the result:

```
Time taken with regular threads: 98614ms
Time taken with virtual threads: 12260ms
```

As you can see, when we increase the number of threads, virtual threads work even better! They take around 12.4% running time of threads.

I was using Java version `21.0.2` on a laptop running windows 11 with 16GB of RAM.