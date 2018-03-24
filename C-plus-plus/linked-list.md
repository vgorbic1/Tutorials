## Linked List
### General Info
There are limitations when you use an array to represent a list of data.  For example,
-	If data is not sorted, searching for an item in the list can be very time consuming.
-	If data is sorted, insertion and deletion become time consuming.
-	The array size must be fixed during execution.

A linked list is a collection of items, called nodes.Each node in a linked list has two 
components: one to store the relevant information, called **info**; and one to store the address, 
called the **link**, of the next node in the list.

There must be a pointer, called the **head** or **first**, to store the address of the first node 
in the list. The link component of the **last** node is assigned to be NULL (points to nothing).

Because each node of a linked list has two components, we need to declare each node as a *class*
or *struct*.  The link component of each node is a pointer, which points to the node type itself:
```c
struct nodeType
{
  int info;
  nodeType * link;
};
nodeType * head;
```
### Traversing a Linked List
When you want to do some action in all of elements of a linked list, you need to have a pointer to 
the first node, and step through the nodes of the list.  It is called *traversing the linked list*:
```c
nodeType * current;
current = head;
while (current != NULL)
{
  // process current
  cout << current->info << endl;
	current = current->link;
}
```
### Insert Item
Suppose that *p* points to the node with *info* 65, and a new node with *info* 50 is to be created 
and inserted after *p*:
```c
nodeType * newNode;
newNode = new nodeType;
assert (newNode != NULL);	// if unable to allocate memory space, terminate the program
newNode->info = 50;
newNode->link = p->link;
p->link = newNode;
```
If we reverse the sequence of the above statements, we don’t get the desired result:
```c
p->link = newNode;
newNode->link = p->link;
```
newNode points back to itself and the remainder of the list is lost.  

We also can use pointers to insert a new node.  Suppose *q* points to the node with *info* 34. The statements 
to insert a new node between *p* and *q*:
```c
newNode->link = q;
p->link = newNode;
```
### Delete Item
Suppose that the node with *info 34* is to be deleted from the list.  The following statements delete the 
node from the list and deallocate the memory occupied by this node:
```c	
q = p->link;
p->link = q->link;
delete q;
```
### Building a Linked List
In the case that the list is not sorted, there are two ways to build the linked list: the forward manner 
(a new node is always inserted at the end of the linked list) and the backward manner (a new node is 
always inserted at the beginning of the linked list).
#### Building a Linked List Forward
Three pointers are needed to build the list: one to point to the first node of the list, which cannot be
moved; one to point to the last node in the list; and one to create the new node.
```c
nodeType * buildListForward()
{
	nodeType * first, * newNode, * last;
	int num;
	cout << "Enter a list of integers ending with -999.\n";
	cin >> num;
	first = NULL;
	while (num != -999) {
		newNode = new nodeType;
		newNode->info = num;
		newNode->link = NULL;
		if (first == NULL) {
			first = newNode;
			last = newNode;
		} else {
			last->link = newNode;
			last = newNode;
		}
		cin >> num;
	}
	return first;
}
```
#### Building a Linked List Backward
Only two pointers are needed to build the list: one to point to the first node of the list, and one to create the new node.
```c
nodeType * buildListBackward()
{
	nodeType * first, * newNode, * last;
	int num;
	cout << "Enter a list of integers ending with -999.\n";
	cin >> num;
	first = NULL;
	while (num != -999) {
		newNode = new nodeType;
		newNode->info = num;
		newNode->link = first;
		first = newNode;		
		cin >> num;
	}
	return first;
}
```
[LOOK AT LINKED LIST AS AN ADT](https://github.com/vgorbic1/Tutorials/edit/master/C-plus-plus/linked-list-adt.md) 
