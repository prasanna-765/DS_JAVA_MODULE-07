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
Developed by: Abinaya A
RegisterNumber: 212223040003
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
