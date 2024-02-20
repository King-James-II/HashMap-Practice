/* This program utilizes Hash and Tree Map to store and sort data within a map data structure.
 * The tree Map function is used to show that data can be sorted automatically but a comparator 
 * can be used to sort in any desired way. A Binary search tree is used to store the data values 
 * from the Tree Map into it then used to display the capital for a state the user enters.*/

//Importing Map and scanner classes so we can use them within the program.
import java.util.HashMap;
import java.util.TreeMap;
import java.util.Map;
import java.util.Scanner;
public class StateHashMap {
	
//The Main method that will drive the entire program.
	public static void main(String[] args) {
		// Setting up a variable to tell the program when to quit and setting up a scanner object.
		int quit = 0;
		Scanner scan = new Scanner(System.in);
		// Initializing the Hash Map with state and capital values.
		Map<String, String> arrayStates = new HashMap<>();
        arrayStates.put("Delaware", "Dover");
        arrayStates.put("Florida", "Tallahassee");
        arrayStates.put("Georgia", "Atlanta");
        arrayStates.put("Hawaii", "Honolulu");
        arrayStates.put("Idaho", "Boise");
        arrayStates.put("Pennsylvania", "Harrisburg");
        arrayStates.put("Rhode Island", "Providence");
        arrayStates.put("Illinois", "Springfield");
        arrayStates.put("Indiana", "Indianapolis");
        arrayStates.put("Iowa", "Des Moines");
        arrayStates.put("Kansas", "Topeka");
        arrayStates.put("Kentucky", "Frankfort");
        arrayStates.put("Louisiana", "Baton Rouge");
        arrayStates.put("Maine", "Augusta");
        arrayStates.put("Maryland", "Annapolis");
        arrayStates.put("Massachusetts", "Boston");
        arrayStates.put("Michigan", "Lansing");
        arrayStates.put("Arizona", "Phoenix");
        arrayStates.put("South Carolina", "Columbia");
        arrayStates.put("Utah", "Salt Lake City");
        arrayStates.put("Vermont", "Montpelier");
        arrayStates.put("Virginia", "Richmond");
        arrayStates.put("Washington", "Olympia");
        arrayStates.put("Alabama", "Montgomery");
        arrayStates.put("Alaska", "Juneau");
        arrayStates.put("West Virginia", "Charleston");
        arrayStates.put("Wisconsin", "Madison");
        arrayStates.put("Arkansas", "Little Rock");
        arrayStates.put("South Dakota", "Pierre");
        arrayStates.put("Tennessee", "Nashville");
        arrayStates.put("Texas", "Austin");
        arrayStates.put("California", "Sacramento");
        arrayStates.put("New York", "Albany");
        arrayStates.put("North Carolina", "Raleigh");
        arrayStates.put("North Dakota", "Bismarck");
        arrayStates.put("Ohio", "Columbus");
        arrayStates.put("Colorado", "Denver");
        arrayStates.put("Connecticut", "Hartford");
        arrayStates.put("Minnesota", "Saint Paul");
        arrayStates.put("Mississippi", "Jackson");
        arrayStates.put("Missouri", "Jefferson City");
        arrayStates.put("Montana", "Helena");
        arrayStates.put("Nebraska", "Lincoln");
        arrayStates.put("Nevada", "Carson City");
        arrayStates.put("New Hampshire", "Concord");
        arrayStates.put("New Jersey", "Trenton");
        arrayStates.put("New Mexico", "Santa Fe");
        arrayStates.put("Oklahoma", "Oklahoma City");
        arrayStates.put("Oregon", "Salem");
        arrayStates.put("Wyoming", "Cheyenne");
		
        //Displaying HashMap to show that the data structure doesn't store these value in order.
		System.out.println("Displaying contents of State and Captial City Hash Map:");
		System.out.println("=======================================================");
		for (Map.Entry<String, String> entry : arrayStates.entrySet()) {
			String state = entry.getKey();
			String capital = entry.getValue();
			System.out.println('"' + state + '"' + ", " + '"' + capital + '"');
			}
		
		//Initializing TreeMap using the HashMap data
		TreeMap<String, String> stateMap = new TreeMap<>(arrayStates);

		//Displaying the Tree Map to show that it automatically sorts the values by key in order.
		System.out.println("\n\nDisplaying contents of State and Captial City Sorted Tree Map:");
		System.out.println("=======================================================");
		for (Map.Entry<String, String> entry : stateMap.entrySet()) {
			String state = entry.getKey();
			String capital = entry.getValue();
			System.out.println('"' + state + '"' + ", " + '"' + capital + '"');
		}
		
		//Initializing the Binary Search Tree and storing each value within the Binary Search Tree.
		BST statebst = new BST();
		for (Map.Entry<String, String> entry : stateMap.entrySet()) {
			statebst.ins(entry.getKey(), entry.getValue());
		}
		BST.disBST(statebst.root);
		
		// Prompt user to enter a state name find it in the binary search tree and display it's 
		// capital to the user until the user quits the program.
		while (quit == 0)
		{
		System.out.println("\nPlease enter a state to display the captial of the state:\nEnter q to"
				+ " quit.");
		System.out.println("========================================================");
		String input = scan.nextLine();
		if (input.equalsIgnoreCase("q")){
			quit++;
			break;
		}
		String capital = statebst.find(input);
		System.out.println(capital);
		}
	}
	
// Node class to initialize each nodes values 
static class Node {
	String key;
	String value;
	Node left;
	Node right;
	public Node (String state, String capital) {
		this.key = state;
		this.value = capital;
		this.left = null;
		this.right = null;
	}
}

// Binary Search Tree class that contains methods that can insert find and display data contained 
// within the tree.
static class BST {
	private Node root;
	
	public BST() {
		this.root = null;
	}
	
	// Inserts nodes and values into the binary search tree using the comparator.
	public void ins(String state, String capital) {
		this.root = insN(this.root, state, capital);
	}
	
	private Node insN(Node root, String state, String capital) {
		if (root == null) {
			return new Node(state, capital);
		}
		
		if (state.compareTo(root.key) < 0) {
			root.left = insN(root.left, state, capital);
		} else if (state.compareTo(root.key) > 0) {
			root.right = insN(root.right, state, capital);
		}
		
		return root;
	}
	
	// Finds the Node and it's value within the binary search tree.
	public String find(String state) {
		Node node = findN(root, state);
		return node != null ? node.value : null;
	}
	
	private Node findN(Node root, String state) {
		if (root == null || root.key.compareToIgnoreCase(state) == 0) {
			return root;
		}
		
		if (state.compareToIgnoreCase(root.key) < 0) {
			return findN(root.left, state);
		} else {
			return findN(root.right, state);
		}
	}
	
	//Displays all values within the binary search tree in order. 
    private static void disBST(Node root) {
        if (root != null) {
            disBST(root.left);
            System.out.println(root.key + " - " + root.value);
            disBST(root.right);
        }
    }
}

}