- 栅栏类似闭锁,但是它们是有区别的. 
  闭锁用来等待事件，而栅栏用于等待其他线程.什么意思呢?就是说闭锁用来等待的事件就是countDown事件,只有该countDown事件执行后所有之前在等待的线程才有可能继续执行;而栅栏没有类似countDown事件控制线程的执行,只有线程的await方法能控制等待的线程执行.
- CyclicBarrier强调的是n个线程，大家相互等待，只要有一个没完成，所有人都得等着。

场景分析:10个人去春游,规定达到一个地点后才能继续前行.代码如下

```
import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

class CyclicBarrierWorker implements Runnable {
    private int id;
    private CyclicBarrier barrier;

    public CyclicBarrierWorker(int id, final CyclicBarrier barrier) {
        this.id = id;
        this.barrier = barrier;
    }

    @Override
    public void run() {
        // TODO Auto-generated method stub
        try {
            System.out.println(id + " th people wait");
            barrier.await(); // 大家等待最后一个线程到达
        } catch (InterruptedException | BrokenBarrierException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
}

public class TestCyclicBarrier {
    public static void main(String[] args) {
        int num = 10;
        CyclicBarrier barrier = new CyclicBarrier(num, new Runnable() {
            @Override
            public void run() {
                // TODO Auto-generated method stub
                System.out.println("go on together!");
            }
        });
        for (int i = 1; i <= num; i++) {
            new Thread(new CyclicBarrierWorker(i, barrier)).start();
        }
    }
}
输出：
1 th people wait
2 th people wait
3 th people wait
4 th people wait
5 th people wait
7 th people wait
8 th people wait
6 th people wait
9 th people wait
10 th people wait
go on together!
```