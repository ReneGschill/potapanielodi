#include <iostream>
#include <ctime>
using namespace std;

const int rows = 10;
const int elements = 10;

int maxships = 10;

int matrix[rows][elements];

void Clear()
{
	for (int i = 0; i < rows; i++)
	{
		for (int j = 0; j < elements; j++)
		{
			matrix[i][j] = 0;
		}
	}
}

void Show()
{
	for (int i = 0; i < rows; i++)
	{
		for (int j = 0; j < elements; j++)
		{
			cout << matrix[i][j] << " ";
		}
		cout << endl;
	}
}

int NumberOfShips()
{
	int c = 0;

	for (int i = 0; i < rows; i++)
	{
		for (int j = 0; j < elements; j++)
		{
			if (matrix[i][j] == 1)
				c++;
		}
	}

	return c;
}

void SetShips()
{
	int s = 0;
	while (s < maxships)
	{
		int x = rand() % rows;
		int y = rand() % elements;
		if (matrix[x][y] != 1)
		{
			s++;
			matrix[x][y] = 1;
		}
	}
}

bool Attack(int x, int y)
{
	if (matrix[x][y] == 1)
	{
		matrix[x][y] = 2;
		return true;
	}
	return false;
}

int main()
{
	srand(time(NULL));
	Clear();
	SetShips();
	int pos1, pos2;
	char prompt;
	while (1)
	{
		cout << "Prosim zadaj lokaciu: "; cin >> pos1 >> pos2;
		if (Attack(pos1, pos2))
			cout << "Trafil si sa :)" << endl;
		else
			cout << "Ziadne lode na tejto pozicii!" << endl;
		cout << "Zostavajuce lode: " << NumberOfShips() << endl;
		cout << "Chces sa vzdat ty slabko? (a/n)? "; cin >> prompt;
		if (prompt == 'a')
			break;
	}
	cout << "Koniec hry!" << endl;
	Show();
	system("pause");
	return 0;
}

