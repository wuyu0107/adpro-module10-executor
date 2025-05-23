## Reflection 1.2

```
// Spawn a task to print before and after waiting on a timer.
    spawner.spawn(async {
        println!("Min's Computer: howdy!");
        // Wait for our timer future to complete after two seconds.
        TimerFuture::new(Duration::new(2, 0)).await;
        println!("Min's Computer: done!");
    });
    println!("Min's Computer: hey hey");
```
![](/images/image1-2.png)

When we execute the program, the output appears in order shown in the picture above. The message with 'hey hey' comes first, followed by a message with 'howdy!', then after 2 second delay, it prints the 'done!' message. This occurs because of the asynchronous task system. 

The main function prints 'hey hey' immediately and spawns an asynchronous task that starts executing and pinrts 'howdy!' before waiting a custom 2-second delay timer. During this wait, the task is paused and allows the executor to manage other existing tasks. After the timer completes, the task resumes and prints 'done!'. 

## Reflection 1.3

### With the drop spawner
![](/images/image1-3_with.png)

With the drop spawner, all tasks are correctly spawned and complete as expected, creating an output with all 'hey hey', 'howdy!', 'done!' messages.

### Without the drop spawner
![](/images/image1-3_without.png)

However, without the drop spawner, the program doesn't end because executor keeps running, thinking that there are more tasks to be assigned. So it continues receiving the task queue endlessly, preventing the program from exiting. 

