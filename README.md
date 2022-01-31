#include <iostream>
#include <string>
#include "19ToDo.h"
using namespace std;

#ifndef TODO
#define TODO


using std::string;
using std::int16_t;

static int positionInList = 0;
static int listSize = 0;

struct MyToDo
{
	string description;
	int priority;
	string dueDate;



};
struct MyToDo ToDoList[100];



bool addToList(string description, int priority, string dueDate)
{


	if (listSize < 101)
	{
		MyToDo y = { description, priority, dueDate };
		ToDoList[listSize] = y;
		listSize++;
		return true;
	}
	else
	{
		return false;
	}

}
bool getNextItem(MyToDo &mytodo)
{
	if (listSize == 0)
	{

		return false;
	}
	else if (listSize < positionInList)
	{
		positionInList = 0;
		mytodo = ToDoList[positionInList];
		positionInList++;
	}
	else
	{
		mytodo = ToDoList[positionInList];
		positionInList++;

	}
}
bool getByPriority(MyToDo matches[100], int search)
{
	int count = 0;
	
	for (int i = 0; i < listSize; i++)
	{
		if (ToDoList[i].priority == search)
		{
			matches[count] = ToDoList[i];
			count++;
		}
	}


		return true;
	
}
void printToDo()
{

	for (int i = 0; i < listSize; i++)
	{

		cout << ToDoList[i].description << endl;
		cout << ToDoList[i].priority << endl;
		cout << ToDoList[i].dueDate << endl;
		cout << "" << endl;
	}
}

bool addToList(string description, int priority, string dueDate);
bool getNextItem(MyToDo &mytodo);
bool getByPriority(MyToDo matches[100], int search);
void printToDo();

int main()
{
	int choice = 0;
	char nextmove = 'y';


	while (nextmove = 'y')
	{
		cout << "This will keep of the things you need to do!" << endl;
		cout << "What would you like to do?" << endl;
		cout << "1. Add to my to do list" << endl;
		cout << "2. Display the next item in my list" << endl;
		cout << "3. Search for activites of a certain priority" << endl;
		cout << "4. Print out my whole list" << endl;

		cin >> choice;

		if (choice == 1)
		{
			string description;
			int priority;
			string dueDate;


			cout << "what is the description of the activity?" << endl;
			cin.ignore();
			getline(cin, description);
			cout << "how urgent is this? rank 1-5. 1 for not really important, 5 for very important" << endl;
			cin >> priority;
			cout << "when is the due date? is day/month format" << endl;
			cin >> dueDate;

			addToList(description, priority, dueDate);
		}
		else if (choice == 2)
		{

			MyToDo y;

			getNextItem(y);

		
			cout <<"Description: " << y.description << endl;
			cout << "Priority :" << y.priority << endl;
			cout << "Due Date :" << y.dueDate << endl;
			

		}
		else if (choice == 3)
		{
			struct MyToDo matches[100];
			int search = 0;

			cout << "Enter a priority level to search for 1-5" << endl;
			cin >> search;

			getByPriority(&matches[100], search);
			for (int i = 0; i < 10; i++)
			{
				cout << "Description: " << matches[i].description << endl;
				cout << "Priority : " << matches[i].priority << endl;
				cout << "Due Date : " << matches[i].dueDate << endl;
			}
		}
		else if (choice == 4)
		{

			printToDo();
		}
		else
		{
			cout << "That was an incorrect choice!" << endl;
		}
		cout << "would you like to keep playing? y for YES" << endl;
		cin >> nextmove;

	}

	cout << "Good job keeping yourself on schedule!" << endl;
	return 0;
}
