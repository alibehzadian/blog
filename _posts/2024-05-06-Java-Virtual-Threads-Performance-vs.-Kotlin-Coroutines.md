!["Java Virtual Threads Performance vs. Kotlin Coroutines"](/images/2024-05-03-Java-Thread-Performance-vs.-Virtual-Threads.png)

In [previous post](https://blog.behzadian.info/2024-05-03/Java-Thread-Performance-vs.-Virtual-Threads), I just did a simple benchmark to compare performance of Java Threads vs. Java Virtual Threads. In this post, I want to compare Java Virtual Threads against Kotlin Coroutines.

This is a very simple test, I create a very huge number of coroutines, each takes 5 seconds to finish. Then I calculate the duration of running app.

This is Kotlin code I used for this benchmark:

```kotlin
package info.behzadian

import kotlinx.coroutines.delay
import kotlinx.coroutines.launch
import kotlinx.coroutines.runBlocking


fun main() = runBlocking {
    val startTime = System.currentTimeMillis()

    val jobs = List(100000) {
        launch {
            delay(5000L)
        }
    }

    jobs.forEach { it.join() }

    val endTime = System.currentTimeMillis()

    println("Total running time: ${endTime - startTime} ms")
}
```

In first run, I started with 100,000 coroutines and this is the result:

```
Total running time: 5302 ms
```

If you compare this result with Java Virtual Threads (9477ms), you will see that it is much faster!

Then, I tried with 200,000 coroutines and this is the result:

```
Total running time: 5415 ms
```

Amazing! I just doubled number of running coroutines and the overhead for those 100,000 corounes is just 100ms!

If we compare this with Java Virtual Threads (12260ms), you will see that winner is Kotlin Coroutines without any doubt!

I was using Kotlin version `1.9.23` and Coroutines version `1.8.0` on a laptop running windows 11 with 16GB of RAM.