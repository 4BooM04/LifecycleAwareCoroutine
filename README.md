# LifecycleAwareCoroutine
Simpe Coroutine wrapper with LifecycleOwner awarenes.

Clone and add as simple android library module for use.

Im planing to add library  to maven repo in some near future.

This wrapper build coroutine that aware of activities and fragments lifecycle and can autocancel on some events, like PAUSE,DESTROY(**default**),STOP

```sh
   asyncUI {
                // this task will autoCancel on On_DESTROY event
                val measureTimeMillis = measureTimeMillis {
                    //this call will block coroutine till gain current result
                    val number = asyncNow {
                        //this call will be executed in background thread context
                        BusinessLogicLayer().doSomeHeavyWorkWithResult1()
                    }
                    val someTask = promice {
                        BusinessLogicLayer().doSomeHeavyWorkWithResult2()
                    }
                    //this call will block coroutine while  other results will be available
                    //this call will be executed in UI thread context
                    println("result is $number ${someTask.await()}}")
                }
                //total time should be near the sum of first call time and max delay time of  other 3 calls
                println("result with total time of : $measureTimeMillis")
            }
        }
```
Wrapper contain coroutine that can execute block of code in UI Thread and make background call with blocking and promices to make some background context aware calls, like network calls, etc.
