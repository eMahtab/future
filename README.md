# Future

A Java Future, java.util.concurrent.Future, represents the result of an asynchronous computation. When the asynchronous task is created, a Java Future object is returned. This Future object functions as a handle to the result of the asynchronous task. Once the asynchronous task completes, the result can be accessed via the Future object returned when the task was started.

Some of Java's built-in concurrency utilities, like e.g. the Java ExecutorService, return a Java Future object from some of their methods. In the case of the ExecutorService, it returns a Future when you submit a Callable for it to execute concurrently (asynchronously)

### Future returned by ExecutorService on submitting a Callback
```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class FutureExample {

    public static void main(String[] args) {
        // Create a thread pool with a single thread
        ExecutorService executorService = Executors.newSingleThreadExecutor();
        // Define a Callable task that returns a result after simulating a delay
        Callable<String> callableTask = () -> {
            System.out.println("Task started...");
            Thread.sleep(8000);  // Simulate a delay (8 seconds)
            return "Task completed!";
        };

        // Submit the task to the executor service and get a Future object
        Future<String> futureResult = executorService.submit(callableTask);
        // Do some other operations here while the task is running
        System.out.println("Doing other work in main...");

        try {
            // Retrieve the result of the task when it's done
            // get() will block if the task is not yet completed
            String result = futureResult.get();
            System.out.println("Result from callable task: " + result);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            // Shut down the executor service
            executorService.shutdown();
        }
    }
}
```
