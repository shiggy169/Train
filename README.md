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
		int countPass = 0;
		Waggon node = head;
		while(node != null){
			countPass += node.getPassengers();
			node = node.getNext();
		}
		return countPass;
	}

	public int getCapacity() {
		int maxCap = 0;
		Waggon node = head;
		while(node != null){
			maxCap += node.getCapacity();
			node = node.getNext();
		}
		return maxCap;
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
		int passengersOn = numberOfPassengers;
		while(node != null){
			int capacity = node.getCapacity();
			int boardedAlready = node.getPassengers();
			int freeSpace = capacity - boardedAlready;
			
			if(freeSpace == 0){
				node = node.getNext();
				continue;
			}else if(freeSpace >= passengersOn){
				node.setPassengers(boardedAlready +  passengersOn);
				break;
			}else if(freeSpace < passengersOn){
				node.setPassengers(boardedAlready + freeSpace);
				passengersOn -= freeSpace;
			}
			node = node.getNext();
		}
		
	}

	public Train uncoupleWaggons(int index) {
		return new Train();
	}

	public void insertWaggon(Waggon waggon, int index) {
	}

	public void turnOver() {
	}

	public void removeWaggon(Waggon waggon) {
	}

	public Waggon getWaggonAt(int index) {
		return null;
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
