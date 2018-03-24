## Doubly Linked List
A doubly linked list is a linked list in which every node has a next pointer and a back pointer.  The next 
pointer contains the address of the next node, and the back pointer contains the address of the previous node.
### Definition of the node
```c
template<class Type>
struct nodeType
{
	Type info;
	nodeType * next;
	nodeType * back;
};

template<class Type>
class doublyLinkedList
{
public:
	const doublyLinkedList<Type>& operator=
				(const doublyLinkedList<Type>&);
	void initializeList();
	bool isEmptyList();
	void destroy();
	void print();
	void reversePrint();
	int length();
	Type front();
Type back();
	bool search(const Type& searchItem);
	void insert(const Type& insertItem);
	void deleteNode(const Type& deleteItem);
	doublyLinkedList();
		doublyLinkedList(const doublyLinkedList<Type>& 
		otherList);
	~doublyLinkedList();
protected:
	int count;
	nodeType<Type> * first;
	nodeType<Type> * last;
private:
	void copyList(const doublyLinkedList<Type>& otherList);
};

// Default Constructor
template<class Type>
doublyLinkedList<Type>::doublyLinkedList()
{
	first = NULL;
	last = NULL;
	count = 0;
}

// IsEmptyList
template<class Type>
bool doublyLinkedList<Type>::isEmptyList()
{
	return (first == NULL);
}

// Destroy List
template<class Type>
void doublyLinkedList<Type>::destroy()
{
	nodeType<Type> * temp;
	while (first != NULL)
	{
		temp = first;
		first = first->link;
		delete temp;
	}
	last == NULL;
	
	count = 0;
}


// Initalize List
template<class Type>
void doublyLinkedList<Type>::initializeList()
{
	destroy();
}

// length of the list
template<class Type>
int doublyLinkedList<Type>::length()
{
	return count;
}

// Print List
template<class Type>
void doublyLinkedList<Type>::print()
{
	nodeType<Type> * current;
	current = first;
	
	while (current != NULL)
	{
		cout<<current->info<<” “;
		current = current->next;
	}
}

// Reverse Print List
template<class Type>
void doublyLinkedList<Type>::reversePrint()
{
	nodeType<Type> * current;
	current = last;
	while (current != NULL)
	{
		cout<<current->info<<” “;
		current = current->back;
	}
}

// Search List
/* This search algorithm is exactly the same as the search algorithm for an ordered linked list */.

// First and Last Element
template<class Type>
Type doubleLlinkedList<Type>::front()
{
	assert(first != NULL);
	return first->info;
}

template<class Type>
Type doubleLinkedList<Type>::back()
{
	assert(last != NULL);
	return last->info;
}

// Insert Node
/* Because we are inserting an item in a doubly linked list, 
the insertion of a node in the list requires the adjustment of
two pointers in certain nodes. Consider four cases:
Case 1:  Insertion in an empty list.  
Case 2:  Insertion at the beginning of a nonempty list.
Case 3:  Insertion at the end of a nonempty list.
Case 4:  Insertion somewhere in a nonempty list.*/
template<class Type>
void doublyLinked List<Type>::insert
(const Type& insertItem)
{
	nodeType<Type> * current;
	nodeType<Type> * trailCurrent;
	nodeType<Type> * newNode;
  	bool found;

	newNode = new nodeType<Type>;
	assert(newNode != NULL);

 	newNode->info = insertItem;
	newNode->next = NULL;
	newNode->back = NULL;

	if(first == NULL)
	{
		first = newNode;
		last = newNode;
		count++;
	}
	else
{
		found = false;
		current = first;
		while (current != NULL && !found)
			if (current->info >= insertItem)
				found = true;
			else
			{
				trailCurrent = current;
				current = current->next;
			}

		if (current == first)
		{
			first->back = newNode;
			newNode->next = first;
			first = mewNode;
			count++;
		}
		else
		{
			if (current != NULL)
			{
				trailCurrent->next = newNode;
				newNode->back = trailCurrent;
				newNode->next = current;
				current->back = newNode;
			}
			else
			{
				trailCurrent->next = newNode;
				newNode->back = trailCurrent;
				last = newNode;
			}
			count++;
		}
	}
}

//Delete Node
We first search the list to see whether the item to be deleted in the list.  If the item is found, we need to adjust two pointers in certain nodes.  Consider four cases:
Case 1:  The list is empty.
Case 2:  The item to be deleted is in the first node of the list, which would require us to 	change the value of the pointer first.
Case 3:  The item to be deleted is somewhere in the list.
Case 4:  The item to be deleted in not in the list.
(See Figures 5-45, 5-46, 5-47)

template<class Type>
void doublyLinkedList<Type>::deleteNode
							(const Type& deleteItem)
{
	nodeType<Type> * current;
	nodeType<Type> * trailCurrent;

	bool found;

	if (first == NULL)
		cout<<”Cannot delete from an empty list”<<endl;
	else
		if (first->info == deleteItem)
		{
			current = first;
			first = first->next;
			if (first != NULL)
				first->back = NULL;
			else
				last = NULL;
			count--;
			delete current;
		}
		else
		{
			found = false;
			current = first;
			
			while (current != NULL && !found)
			  	if (current->info >= deleteItem)
					found = true;
				else
					current = current->next;

			if (current == NULL)
				cout<<”The item to be deleted is not "
        << ”in the list.” << endl;
			else
				if (current->info == deleteItem)
				{
					trailCurrent = current->back;
					trailCurrent->next=current->next;

					if (current->next != NULL)
					 current->next->back=trailCurrent;
					if (current == last)
						last = trailCurrent;

					count--;
					delete current;
				}
				else
					cout<<"The item to be deleted "
					   << "is not in the list." << endl;
		}
	}
}
```
