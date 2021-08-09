```java
class PrintTask {
	boolean odd;
	int num = 1;
	int max = 20;

	public void printOdd() {
		synchronized (this) {
			while (num < max) {
				while (!odd) {
					try {
						wait();
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				}
				odd = false;
				System.out.println("Odd thread :: " + num);
				num++;
				notify();
			}
		}
	}

	public void printEven() {
		synchronized (this) {
			while (num < max) {
				while (odd) {
					try {
						wait();
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				}
				System.out.println("Even thread :: " + num);
				num++;
				odd = true;
				notify();
			}
		}
	}
}

public class PracticeClass {
	public static void main(String[] args) {
		PrintTask p = new PrintTask();
		p.odd = true;
//		Thread t1 = new Thread(()->{p.printOdd();});
//		Thread t2 = new Thread(()->{p.printEven();});
//		
//		t1.start();
//		t2.start();

		ExecutorService e = Executors.newFixedThreadPool(2);
		e.execute(() -> {
			p.printOdd();
		});
		e.execute(() -> {
			p.printEven();
		});

		e.shutdown();
	}

}
```
