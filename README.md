doublylinkedlist
================
// DoublyLinkedList.java 

class DoublyLinkedList{
	private int N=0;
	private Node first;
	private Node last;

	public class Node {
		private int data;
		private Node next;
		public Node previous;
		
		public Node (int data) {
			this.data= data;
		}
		public int getdata(){
			return this.data;
		}
		public void showdata(){
			System.out.println(this.getdata() + "");
		}
	}

	public DoublyLinkedList (){
		this.first= null;
		this.last= null;
	}
	public boolean isEmpty (){
		return (this.N ==0);
	}
	public int size (){
		return this.N ;
	}
	public void showSize(){
		System.out.println("Show Size of the DoublyLinkedList");
	}

	public void insertFirst(int value){
		Node newNode = new Node(value);
		if (this.isEmpty ())
				this.last = newNode;
		else {
			this.first.previous = newNode;
		}
		newNode.next = first;
		this.first = newNode;
		this.N++;
	}

	public void insertLast(int value){
		Node newNode = new Node(value);
		if (this.isEmpty()) {
			this.first = newNode;
		} else {
			this.last.next= newNode;
			newNode.previous= this.last;
		}
		this.last = newNode;
		this.N++;
	}
	public Node deleteFirst() {
		Node temp = this.first;
		if (this.first.next == null) {
			this.last = null;
		} else {
			this.first.next.previous = null;
		}
		this.first = first.next;
		this.N--;
		return temp;
	}

	public Node deleteLast() {
		Node temp = this.last;
		if (this.first.next == null) {
			this.first = null;
		} else {
			this.last.previous.next = null;
		}
		this.last = this.last.previous;
		this.N--;
		return temp;
	}

	public Boolean insertAfter(int key, int value) {
		Node current = this.first;
		while (current.getdata() != key) {
			current = current.next;
			if (current == null) {
				return false;
			}
		}
		Node newNode = new Node(value);
		if (current == this.last) {
			newNode.next = null;
			this.last = newNode;
		} else {
			newNode.next = current.next;
			current.next.previous = newNode;
		}
		if (current == this.last) {
			newNode.next = null;
		} else {
			newNode.next = current.next;
			current.next.previous = newNode;
		}
		newNode.previous = current;
		current.next = newNode;
		this.N++;
		return true;
	}

	
	public Node deletekey(int key){
		Node current = first;
		while (current.getdata()!= key) {
			current = current.next;
			if (current ==null) {
				return null;
			}
		}
		if (current ==this.first) {
			this.first = current.next;
		} else {
			current.next.previous = current.previous;
		}	

		if (current ==this.first) {
			this.last = current.previous;
		} else {
			current.next.previous = current.previous;
		}	
		this.N--;
		return current;
	}
	public void displaybackward(){
		System.out.println("displaybackward (last --> first)");
		Node current = this.last;
		while (current != null) {
			current.showdata();
			current = current.previous;
		}
		
	}
	public void displayforward(){
		System.out.println("displayforward (first --> last)");
		Node current = this.first;
		
		while (current != null) {
			current.showdata();
			current = current.next;
		}
		System.out.print("");
	}



}

// Tester.java

//latest example ni sir
class Tester{
	public static void main(String[] args) {
		
		DoublyLinkedList  list = new DoublyLinkedList();
		list.insertFirst(3);
		list.insertFirst(8);
		list.insertFirst(12);
		list.insertLast(12);
		list.insertLast(13);
		list.insertLast(14);

		list.displayforward();
		list.displaybackward();

		list.deleteFirst();
		System.out.println("first node deleted");
		list.displayforward();
		list.deleteLast();
		System.out.println("last node deleted");
		list.displayforward();
		list.deletekey(12);
		System.out.println("12 node deleted");
		list.displayforward();
		list.insertAfter(8,7);
		System.out.println(" 7 node inserted after 8");
		list.insertAfter(3,5);
		System.out.println(" 5 node inserted after 8");
		list.deletekey(12);
		System.out.println("12 node deleted");
		list.displayforward();
		
	}
}

