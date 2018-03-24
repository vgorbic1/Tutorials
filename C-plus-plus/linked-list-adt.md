## Linked List As an ADT
The basic operations on linked lists are:
1. Initialize the list
2. Check whether the list is empty
3. Output the list
4. Find the length of the list
5. Destroy the list
6. Retrieve the info contained in the first node
7. Retrieve the info contained in the last node
8. Search the list for a given item
9. Insert an item in the list
10. Delete an item from the list
11. Make a copy of the linked list
### Definition of the node
```c
template<class Type>
struct nodeType
{
	Type info;
	nodeType<Type> * link;
};

template<class Type>
class linkedListType
{
	friend ostream& operator<<(ostream&, const linkedlistType<Type>&);
public:
	const linkedListType<Type>& operator=(const linkedListType<Type>&);
	void initializeList();
	bool isEmptyList();
	int length();
	void destroyList();
	Type front();
	Type back();
	bool search(const Type& searchItem);
	void insertFirst(const Type& newItem);
	void insertLast(const Type& newitem);
	void deleteNode(const Type& deleteItem);
	linkedListType();
	linkedListType(const linkedListType<Type>& otherList);
	~linkedListType();
protected:
	int count;
	nodeType<Type> * first;
	nodeType<Type> * last;
private:
	void copyList(const linkedListType<Type>& otherList);
};
```
The definitions of the functions in the linkedListType class are:
```c
// Default Constructor. (big-O(1))
template<class Type>
linkedListType<Type>::linkedListType()
{
	first = NULL;
	last = NULL;
	count = 0;
}

// Determine whether the list is empty. (big-O(1))
template<class Type>					
bool linkedListType<Type>::isEmptyList()
{
	return (first == NULL);
}

// Length of the List. (big-O(1))
template<class Type>					
int linkedListType<Type>::length()
{
	return count;
}

// Destroy List. (big-O(n))
template<class Type>					
void linkedListType<Type>::destroyList()
{
	nodeType<Type> * temp;
	while (first != NULL)
	{
		temp = first;
		first = first->link;
		delete temp;
	}
	
	last = NULL;
	count = 0;
}

// Initialize List – this operation reinitializes the list to an empty state. (big-O(n))
template<class Type>					
void linkedListType<Type>::initializeList()
{
	destroyList();
}
	
// Overloading the Stream Insertion Operator <<. (big-O(n))
template<class Type>
ostream& operator<<(ostream& osObject, 
			const linkedListType<Type>& list)
{
	nodeType<Type> * current;
	current = list.first;
	while (current != NULL)
	{
		osObject<<current->info<<” “;
		current = current->link;
	}
	return osObject;
}


// Retrieve Data of the First Node. (big-O(1))
template<class Type>	
Type linkedListType<Type>::front()
{
	assert(last != NULL);
	return first->info;
}

// Retrieve Data of the Last Node. (big-O(1))
template<class Type>					
Type linkedListType<Type>::back()
{
	assert(last != NULL)
	return last->info;
}

// Insert First Node. (big-O(1))
template<class Type>
void linkedListType<Type>::insertFirst(const Type& newItem)
{
	nodeType<Type> * newNode;
	newNode = new nodeType<Type>;
	assert(newNode != NULL);
	newNode->info = newItem;
	newNode->link = first;
	first = newNode;
	count++;
	
	if (last == NULL)
		last = newNode;
};

// Insert Last Node. (big-O(1))
template<class Type>
void linkedListType<Type>::insertLast(const Type& newItem)
{
	nodeType<Type> * newNode;
	newNode = new nodeType<Type>;
	assert(newNode != NULL);
	
	newNode->info = newItem;
	newNode->link = NULL;

	if (first == NULL)
	{
		first = newNode;
		last = newNode;
		count++;
	}
	else
	{
		last->link = newNode;
		last = newNode;
		count++;
	}
}

// Search List. (big-O(n))
template<class Type>
bool linkedListType<Type>::search(const Type& searchItem)
{
	nodeType<Type> * current;
	bool found;

	current = first;
	found = false;
	while (current != NULL && !found)
		if (current->info == searchItem)
			found = true;
		else
			current = current->link;
	
	return found;
};

// Delete Node. (big-O(n))
/* Consider several cases:
Case 1:  The list is empty.
Case 2:  The node to be deleted is the first node.
	Case 2a:  The list has only one node.
	Case 2b:  The list has more than one node.
Case 3:  The node to be deleted is not the first node, but is somewhere in this list.
	Case 3a:  The node to be deleted is not the last node.
	Case 3b:  The node to be deleted is the last node.
Case 4:  The node to be deleted is not in the list.
*/
template<class Type>
void linkedListType<Type>::deleteNode
						(const Type& deleteItem)
{
	nodeType<Type> * current;
	nodeType<Type> * trailCurrent;
	bool found;

	if (first == NULL)
		cout<<”Cannot delete from an empty list.\n”;
	else
	{
		if (first->info == deleteItem)
		{
			current = first;
			first = first->link;
			count--;
			if (first == NULL)
				last = NULL;
			delete current;
		}
		else
		{
			found = false;
			trailCurrent = first;
			current = first->link;
			
			while (current != NULL && !found)
			{
				if (current->info != deleteItem)
				{
					trailCurrent = current;
					current = current->link;
				}
				else
					found = true;
			}

			if (found)
			{
				trailCurrent->link = current->link;
				count--;
				if (last == current)
					last = trailCurrent;
				
				delete current;
			}
			else
				cout<<”Item to be deleted is not in ”
					<< “the list.”<< endl;
      }
   }
}

// Copy List. (big-O(n))
template<class Type>					
void linkedListType<Type>::copyList
			(const linkedListType<Type>& otherList)
{
	nodeType<Type> * newNode;
	nodeType<Type> * current;

	if (first != NULL)
		destroyList();

	if (otherList.first == NULL)
	{
		first = NULL;
		last = NULL;
		count = 0;
	}
	else
	{
		current = otherList.first;
		count = otherList.count;
		first = new nodeType<Type>;
		assert(first != NULL);

		first->info = current->info;
		first->link = NULL;

		last = first;
		
		current = current->link;
		while (current != NULL)
		{
			newNode = new nodeType<Type>;
			assert(newNode != NULL);

			newNode->info = current->info;
			newNode->link = NULL;
			last->link = newNode;
			last = newNode;
			current = current->link;
}}}

// Destructor. (big-O(n))
template<class Type>
linkedListType<Type>::~llinkedListType()
{
	destroyList();
}

// Copy Constructor. (big-O(n))
template<class Type>
linkedListType<Type>::linkedlistType
			(const linkedListType<Type>& otherList)
{
	first = NULL;
	copyList(otherList);
}

// Overloading the assignment Operator. (big-O(n))
template<class Type>				
const linkedListType<Type>& linkedListType<Type>::operator=
			(const linkedListType<Type>& otherList)
{
	if (this != &otherList)
		copyList(otherList);

	return * this;
}
```
