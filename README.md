# Doubly-linked-list
#include <iostream>
#include <cstdlib> // For malloc and free
using namespace std;


// Define the structure for a node in the doubly linked list
struct Node {
    int data;
    Node* prev;
    Node* next;
};


// Function to insert a node at the end of the doubly linked list
void insertAtEnd(Node*& head, int value) {
    // Allocate memory for a new node using malloc
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == nullptr) {
        cout << "Memory allocation failed!" << endl;
        return;
    }
    newNode->data = value;
    newNode->prev = nullptr;
    newNode->next = nullptr;


    // If the list is empty, make the new node the head
    if (head == nullptr) {
        head = newNode;
        cout << "Inserted " << value << " at the end (it's the first node).\n";
        return;
    }


    // Traverse to the last node
    Node* temp = head;
    while (temp->next != nullptr) {
        temp = temp->next;
    }


    // Update pointers to insert the new node at the end
    temp->next = newNode;
    newNode->prev = temp;


    cout << "Inserted " << value << " at the end.\n";
}


// Function to delete a node from the beginning of the doubly linked list
void deleteFromBeginning(Node*& head) {
    if (head == nullptr) {
        cout << "List is empty. Cannot delete.\n";
        return;
    }


    Node* temp = head;
    head = head->next;


    // Update the previous pointer of the new head
    if (head != nullptr) {
        head->prev = nullptr;
    }


    free(temp); // Free the memory allocated for the node
    cout << "Node deleted from the beginning.\n";
}


// Function to display the doubly linked list
void displayList(Node* head) {
    if (head == nullptr) {
        cout << "List is empty.\n";
        return;
    }
    Node* temp = head;
    cout << "List: ";
    while (temp != nullptr) {
        cout << temp->data << " ";
        temp = temp->next;
    }
    cout << endl;
}


// Main function to demonstrate insertion and deletion
int main() {
    Node* head = nullptr; // Initially, the list is empty


    // Display the empty list
    displayList(head);


    // Insert nodes at the end
    insertAtEnd(head, 10);
    insertAtEnd(head, 20);
    insertAtEnd(head, 30);
    displayList(head);


    // Delete nodes from the beginning
    deleteFromBeginning(head);
    displayList(head);


    deleteFromBeginning(head);
    displayList(head);


    // Delete when the list is empty
    deleteFromBeginning(head);


    return 0;
}
