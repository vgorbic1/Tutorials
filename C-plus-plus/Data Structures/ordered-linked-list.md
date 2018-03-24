## Ordered Linked List
The following operations are usually performed on an ordered list:
1)	Initialize the list.
2)	Check whether the list is empty.
3)	Output the list.
4)	Output the list in the reverse order.
5)	Destroy the list.
6)	Search the list for a given item.
7)	Insert an item in the list.
8)	Delete an item from the list.
9)	Find the length of the list.
10)	Make a copy of the list.

Many of the operations on ordered linked lists are similar to the operations on the operations on unsorted lists.  
We only need to modify the *search*, *insert*, and *delete* operations. Therefore, we derive the class to define 
the ordered linked list as an ADT from the class `linkedListType`.
```c
template<class Type>
class orderedLinkedListType: public linkedListType<Type>
{
public:
	bool search(const Type& searchItem);
	void insert(const Type& newItem);
void insertFirst(const Type& newItem);
	void insertLast(const Type& newItem);
	void deleteNode(const Type& deleteItem);
};
```
### Search List
We start the search at the first node; and stop the search when we either find a node in the list with the 
info greater than or equal to the search item, or we have searched the entire list:
```c
template<class Type>
bool orderedLinkedListType<Type>::search(const Type& searchItem)
{
	bool found;
	nodeType<Type> * current;

	found = false;
	current = first;
	while (current != NULL && !found)
		if (current->info >= searchItem)
			found = true;
		else
			current = current->link;

	if (found)
		found = (current->info == searchItem);

	return found;
}
```

### Insert Node
To insert an item in an ordered linked list, we first find the place where the new item is supposed to go, and then insert it in the list.  Here we use two pointers, current and trailCurrent.  The pointer current points the node whose info is being compared with the item to be inserted; trailCurrent points to the node just before current.  We consider several cases (see Figures 5-34 – 5-41):
- Case 1:  The list is empty.
- Case 2:  The list is not empty, and the new item is smaller than the smallest (first) item in the list.
- Case 3:  The list is not empty, and the new item is larger than the first item in the list. 
- Case 3a:  The new item is inserted at the end of in the list.
- Case 3b:  The new item is inserted somewhere in the middle of the list.
```c
template<class Type>
void orderedLinkedlistType<Type>::insert
							(const Type& newitem)
{
	nodeType<Type> * current;
	nodeType<Type> * trailCurrent;
	nodeType<Type> * newNode;
	bool found;
	
	newNode = new nodeType<Type>;
	assert(newNode != NULL);
	newNode->info = newItem;
	newNode->link = NULL;

	if (first == NULL)
	{
		first = newNode;	last = newNode;
		count++;
	}
	else
	{
		current = first;
		found = false;

		while (current != NULL && !found)
			if (current->info >= newitem)
				found = true;
			else
			{
				trailCurrent = current;
        current = current->link;
			}

		if (current == first)
		{
			newNode->link = first;
			first = newNode;
			count++;
		}
		else
		{
			trailCurrent->link = newNode;
			newNode->link = current;
			if (current == NULL)
				last = newNode;
			count++;
		}
  }
}
```
### Delete Node
Consider four cases:
- Case 1:  The list is empty.
- Case 2:  The item to be deleted is the first node of the list.
- Case 3:  The item to be deleted is somewhere in the list.
- Case 4:  The list is not empty, but the item to be deleted in not in the list.
```c
template<class Type>
void orderedLinkedListType<Type>::deleteNode(const Type& deleteItem)
{
	nodeType<Type> * current;
	nodeType<Type> * trailCurrent;
	bool found;

	if (first == NULL)
		cout << ”Cannot delete from an empty list.\n”;
	else
	{
		current = first;
		found = false;

		while (current != NULL && !found)
			if (current->info >= newitem)
				found = true;
			else
			{
				trailCurrent = current;								current = current->link;
			}
		
		if (current == NULL)
			cout<<”The item to be deleted is not in the”
				<< “ list.\n”;
		else
			if (current->info == deleteItem)
			{
				if (first == current)
				{
					first = first->link;
					if (current->link == NULL)
						last = NULL;
					delete current;
				}
				else
				{
					trailCurrent->link=current->link;
					if (current->link == NULL)
						last = trailCurrent;
delete current;
				}
			count--;
		}
		else
			cout << ”The item to be deleted is not in the”
				<<”list.\n”;
		}
	}
}
```
