# Ex6 Right Rotation LinkedList

## AIM:
To write a Java  program to:
Create a singly linked list.
Rotate the linked list to the right by k positions.
Display the rotated linked list.
## Algorithm
1. Start the program.
2. Define a Node class consisting of data and a reference next.
3. Create a LinkedList class with methods to:
4. Insert nodes at the end.
5. Rotate the list to the right by k positions.
6. Display the list.
7. Read the number of nodes and insert them into the linked list.
8. Read the value of k (number of rotations).
To rotate:

Count the total number of nodes (len).

Make the list circular by connecting the last node to the head.

Compute k = k % len to avoid unnecessary rotations.

Traverse to the (len - k - 1)th node and set the new head.

Break the circular connection.

9. Display the rotated list.
10. Stop the program.
  
## Program:
```
/*
Program to  Right Rotation LinkedList
Developed by: PRASANNA A
RegisterNumber: 212223040078
*/
import java.util.Scanner;

class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    Node head;

    // Insert node at end
    public void insert(int data) {
        Node newNode = new Node(data);

        if (head == null) {
            head = newNode;
        } else {
            Node temp = head;
            while (temp.next != null)
                temp = temp.next;
            temp.next = newNode;
        }
    }

    // Right rotate linked list by k positions
    public void rightRotate(int k) {
        if (head == null || k == 0)
            return;

        Node temp = head;
        int len = 1;

        while (temp.next != null) {
            temp = temp.next;
            len++;
        }

        // Make circular
        temp.next = head;

        k = k % len;  // Effective rotation
        int stepsToNewHead = len - k;

        Node newTail = temp;
        while (stepsToNewHead-- > 0) {
            newTail = newTail.next;
        }

        head = newTail.next;
        newTail.next = null;
    }

    // Display list
    public void display() {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }
}

public class RightRotationLinkedList {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        LinkedList list = new LinkedList();

        System.out.print("Enter number of nodes: ");
        int n = sc.nextInt();

        System.out.println("Enter " + n + " elements:");
        for (int i = 0; i < n; i++) {
            list.insert(sc.nextInt());
        }

        System.out.print("Enter k (positions to rotate): ");
        int k = sc.nextInt();

        list.rightRotate(k);

        System.out.println("Rotated Linked List:");
        list.display();

        sc.close();
    }
}
```

## Output:

<img width="571" height="232" alt="image" src="https://github.com/user-attachments/assets/8072a993-dd5b-4420-ab99-e785cae1316a" />


## Result:
Thus, the java program to perfom right rotation on linked list is implemented successfully.

# Ex7 Removal of Nodes with a Specific Value from a Linked List

## DATE:

## AIM:
To write a Java program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.

## Algorithm
1. Start the program.  
2. Define a `Node` class containing `data` and `next`.  
3. Create a linked list by inserting elements.  
4. Traverse the list and remove nodes whose data equals the specified value.  
5. Adjust pointers to skip deleted nodes and maintain the linked list.  
6. Display the modified linked list.  
7. Stop the program.  

## Program:
```java
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by: PRASANNA A
RegisterNumber:  212223220078
*/
import java.util.Scanner;

class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class RemoveValueLinkedList {
    static Node removeElements(Node head, int val) {
        while (head != null && head.data == val) {
            head = head.next;
        }
        Node current = head;
        while (current != null && current.next != null) {
            if (current.next.data == val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }
        return head;
    }

    static void display(Node head) {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Node head = null, tail = null;
        System.out.print("Enter number of elements: ");
        int n = sc.nextInt();
        System.out.println("Enter elements:");
        for (int i = 0; i < n; i++) {
            int val = sc.nextInt();
            Node newNode = new Node(val);
            if (head == null) {
                head = tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }
        System.out.print("Enter value to remove: ");
        int value = sc.nextInt();
        head = removeElements(head, value);
        System.out.println("Linked list after removal:");
        display(head);
        sc.close();
    }
}
```
## OUTPUT
<img width="943" height="209" alt="image" src="https://github.com/user-attachments/assets/a053d010-8c86-4f35-80da-051e624e5273" />

## RESULT
Thus, The Java program successfully removes all nodes with the specified value (val) from the linked list and returns the new head.


# Ex8 Detection of Cycle and Finding the Starting Node in a Linked List


## AIM:
To write a Java program that detects a cycle in a linked list and returns the node where the cycle begins.  
If there is no cycle, the program should return null without modifying the linked list.

## Algorithm
1. Start the program.  
2. Define a `Node` class containing `data` and `next`.  
3. Create a linked list and manually introduce a cycle for testing.  
4. Use Floyd’s Cycle Detection Algorithm (Tortoise and Hare method):  
   - Move one pointer (`slow`) one step and another (`fast`) two steps.  
   - If they meet, a cycle exists.  
5. To find the start node of the cycle, reset one pointer to the head and move both one step at a time until they meet again.  
6. Display the starting node of the cycle, or print “No cycle detected.” if none exists.  
7. Stop the program.  

## Program:
```java
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by: PRASANNA A
RegisterNumber:  212223040078
*/
class Node {
    int data;
    Node next;
    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class DetectCycleLinkedList {
    static Node detectCycle(Node head) {
        Node slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                Node entry = head;
                while (entry != slow) {
                    entry = entry.next;
                    slow = slow.next;
                }
                return entry;
            }
        }
        return null;
    }

    public static void main(String[] args) {
        Node head = new Node(1);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = new Node(4);
        head.next.next.next.next = new Node(5);

        head.next.next.next.next.next = head.next.next; // Create cycle

        Node cycleStart = detectCycle(head);
        if (cycleStart != null)
            System.out.println("Cycle detected at node with value: " + cycleStart.data);
        else
            System.out.println("No cycle detected.");
    }
}
```
## OUTPUT
<img width="943" height="60" alt="image" src="https://github.com/user-attachments/assets/fc168040-99e7-4eed-adbd-c8abfa211799" />

## RESULT
The program successfully detects whether a cycle exists in the linked list.
If a cycle is present, it correctly identifies and returns the node where the cycle begins.

# Ex9 Finding the Longest Length of Nested Set in a Permutation Array

## DATE:

## AIM:
To write a program that finds the length of the longest set s[k] defined as  
s[k] = { nums[k], nums[nums[k]], nums[nums[nums[k]]], … }  
where the iteration stops before a duplicate element occurs. The task is to return the maximum size among all such sets.

## Algorithm
1. Start the program.  
2. Read the number of elements and the permutation array.  
3. Create a boolean `visited` array initialized to false.  
4. For each index `i` not yet visited, follow the chain `x = nums[x]`, marking visited elements and counting steps until revisiting; this gives the size of s[i].  
5. Track the maximum size encountered.  
6. Output the maximum size.  
7. Stop the program.

## Program:
```java
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by : PRASANNA A
RegisterNumber:  212223040078
*/
import java.util.Scanner;

public class LongestNestedSet {
    static int arrayNesting(int[] nums) {
        int n = nums.length;
        boolean[] visited = new boolean[n];
        int maxSize = 0;
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                int size = 0;
                int current = i;
                while (!visited[current]) {
                    visited[current] = true;
                    current = nums[current];
                    size++;
                }
                if (size > maxSize) maxSize = size;
            }
        }
        return maxSize;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of elements: ");
        int n = sc.nextInt();
        int[] nums = new int[n];
        System.out.println("Enter the permutation array elements (0-based indices):");
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        int result = arrayNesting(nums);
        System.out.println("Longest length of nested set: " + result);
        sc.close();
    }
}
```
## OUTPUT
<img width="927" height="151" alt="image" src="https://github.com/user-attachments/assets/566b48c5-e998-4d5a-8ecf-8b3f06f7222e" />

## RESULT
The program successfully computes the longest length of the nested set s[k] for the given permutation array.

# Ex10 Flattening a Nested List Using an Iterator

## DATE:

## AIM:
To design and implement a class `NestedIterator` that flattens a nested list of integers such that all integers can be accessed sequentially using an iterator interface (`next()` and `hasNext()`).

## Algorithm
1. Start the program.  
2. Define an interface-like class `NestedInteger` that can represent either a single integer or a nested list.  
3. Use a stack or recursion to flatten all integers from the nested list into a single list.  
4. Store the flattened list and maintain an index to track the current element.  
5. Implement `next()` to return the next integer and `hasNext()` to check if more integers exist.  
6. Test the iterator with a sample nested list.  
7. Stop the program.  

## Program:
```java
/*
program that removes all nodes from a linked list whose value matches a given integer (val) and returns the new head of the modified linked list.
Developed by: PRASANNA A
RegisterNumber:  212223040078
*/
import java.util.*;

interface NestedInteger {
    boolean isInteger();
    Integer getInteger();
    List<NestedInteger> getList();
}

class NI implements NestedInteger {
    private Integer value;
    private List<NestedInteger> list;

    NI(Integer value) {
        this.value = value;
        this.list = null;
    }

    NI(List<NestedInteger> list) {
        this.list = list;
        this.value = null;
    }

    public boolean isInteger() {
        return value != null;
    }

    public Integer getInteger() {
        return value;
    }

    public List<NestedInteger> getList() {
        return list;
    }
}

class NestedIterator implements Iterator<Integer> {
    private List<Integer> flattenedList = new ArrayList<>();
    private int index = 0;

    public NestedIterator(List<NestedInteger> nestedList) {
        flatten(nestedList);
    }

    private void flatten(List<NestedInteger> nestedList) {
        for (NestedInteger ni : nestedList) {
            if (ni.isInteger()) {
                flattenedList.add(ni.getInteger());
            } else {
                flatten(ni.getList());
            }
        }
    }

    public Integer next() {
        return flattenedList.get(index++);
    }

    public boolean hasNext() {
        return index < flattenedList.size();
    }
}

public class FlattenNestedList {
    public static void main(String[] args) {
        List<NestedInteger> nestedList = new ArrayList<>();
        nestedList.add(new NI(1));
        List<NestedInteger> innerList = new ArrayList<>();
        innerList.add(new NI(2));
        innerList.add(new NI(3));
        nestedList.add(new NI(innerList));
        nestedList.add(new NI(4));

        NestedIterator i = new NestedIterator(nestedList);
        System.out.print("Flattened list: ");
        while (i.hasNext()) {
            System.out.print(i.next() + " ");
        }
    }
}
```
## OUTPUT
<img width="949" height="67" alt="image" src="https://github.com/user-attachments/assets/9e88a4ec-8c02-403d-a67d-9c5af0fbcda1" />

## RESULT
The NestedIterator class successfully flattens a nested list of integers into a single list and provides sequential access using standard iterator methods.
