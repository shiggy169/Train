# Train
public class Train {

	// Kann für die Ausgabe verwendet werden
	private static final String LOCOMOTIVE = "<___|o|";

	private Waggon head;

	public int getSize() {
		int size = 0;
		Waggon node = head;
		while(node != null){
			size++;
			node = node.getNext();
		}
		return size;
	}

	public int getPassengerCount() {
		int counter = 0;
		Waggon node = head;
		while(node != null){
			counter += node.getPassengers();
			node = node.getNext();
		}
		return counter;
	}

	public int getCapacity() {
		int capacity = 0;
		Waggon node = head;
		while(node != null){
			capacity += node.getCapacity();
			node = node.getNext();
		}
		return capacity;
	}

	public void appendWaggon(Waggon waggon) {
		if(getSize() == 0){
			head = waggon;
		}else{
			Waggon node = head;
			int size = getSize();
			for(int i = 1; i < size; i++){
				node = node.getNext();
			}
			node.setNext(waggon);
		}	
	}

	public void boardPassengers(int numberOfPassengers) {
		Waggon node = head;
		int passengersNo = numberOfPassengers;
		
		while(node != null){
			int cap = node.getCapacity();
			int passIn = node.getPassengers();
			int freeSpace = cap - passIn;
			
			if(freeSpace == 0){
				node = node.getNext();
				continue;
			}else if(freeSpace >= passengersNo){
				node.setPassengers(passIn + passengersNo);
				break;
			}else if(freeSpace < passengersNo){
				node.setPassengers(passIn + freeSpace);
				passengersNo -= freeSpace;
			}
			node = node.getNext();
		}
	}

	public Train uncoupleWaggons(int index) {
		if(index < 0 || index > getSize()){
			return null;
		}else{
			Train tempTrain = new Train();
			Waggon node = getWaggonAt(index - 1);
			Waggon next = node.getNext();
			node.setNext(null);
			tempTrain.head = next;
			
			return tempTrain;
		}
	}

	public void insertWaggon(Waggon waggon, int index) {
		if(waggon == null || index < 0){}
		else if(index == 0){
			Waggon next = head;
			head = waggon;
			head.setNext(next);
		}else if(index >= getSize()){
			Waggon node = getWaggonAt(index - 1);
			node.setNext(waggon);
		}else{
			Waggon prev = getWaggonAt(index - 1);
			Waggon next = getWaggonAt(index);
			prev.setNext(waggon);
			waggon.setNext(next);
		}
	}

	public void turnOver() {
		Waggon newHead = getWaggonAt(getSize() - 1);
		Train tempTrain = new Train();
		while(getSize() > 0){
			newHead = getWaggonAt(getSize() - 1);
			tempTrain.appendWaggon(newHead);
			removeWaggon(newHead);
		}
		head = tempTrain.getWaggonAt(0);
	}

	public void removeWaggon(Waggon waggon) {
		if(waggon == null){}
		else{
			if(head == waggon){
				head = head.getNext();
			}else{
				Waggon node = head;
				while(node != null && node.getNext() != waggon){
					node = node.getNext();
				}
				if(node != null){
					node.setNext(node.getNext().getNext());
				}
			}
		}
	}

	public Waggon getWaggonAt(int index) {
		if(index < 0 || index > getSize()){
			return null;
		}else{
			Waggon node = head;
			for(int i = 0; i < index; i++){
				node = node.getNext();
			}
			return node;
		}
	}

	@Override
	public String toString() {
		if (getSize() == 0) {
			return LOCOMOTIVE;
		}

		StringBuilder str = new StringBuilder(LOCOMOTIVE);

		Waggon pointer = head;
		while (pointer != null) {
			str.append(" <---> ");
			str.append(pointer.getName());
			pointer = pointer.getNext();
		}

		return str.toString();
	}

}
