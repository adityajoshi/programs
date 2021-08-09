```java
import java.util.Optional;

public class LinkedListMiddleElement {

	public static void main(String[] args) {
		Element head = createList();
		Optional<String> middle = findMiddle(head);
		middle.ifPresent(System.out::println);
	}
	
	public static Optional<String> findMiddle(Element head){
		Element fastPointer = head;
		Element slowPointer = head;
		
		while(fastPointer.hasNext() && fastPointer.getNext().hasNext()) {
			fastPointer = fastPointer.getNext().getNext();
			slowPointer = slowPointer.getNext();
		}
		return Optional.ofNullable(slowPointer.getData());
	}

	// Creating list of 10 elements
	public static Element createList() {
		Element head = new Element("1");
		Element current = head;
		
		for(int i=2;i<=10;i++) {
			Element newNode = new Element(String.valueOf(i));
			current.setNext(newNode);
			current = newNode;
		}
		return head;
	}
}

class Element {
	private String data;
	private Element next;

	public String getData() {
		return data;
	}

	public void setData(String data) {
		this.data = data;
	}

	public Element getNext() {
		return next;
	}

	public void setNext(Element next) {
		this.next = next;
	}

	public Element(String data) {
		super();
		this.data = data;
		this.next = null;
	}

	public boolean hasNext() {
		return next != null;
	}

}
```
