#include <iostream>
#include <fstream>
#include "Header.h"

bool DFS(Graph& g);
bool dfs(Graph& g, int* check, int i);

bool DFS(Graph& g)
{
	int n = g.get_size();
	int* check = new int[n];
	for (int i = 0; i < n; i++)
		check[i] = 0;
	for (int i = 0; i < n; i++)
	{
		if (!check[i])
		{
			if (dfs(g, check, i) == 0)
				return 1;
		}
	}
	return 0;
}

int K(Graph& g, int* check, int i)
{
	int k = 0;
	for (int i = 0; i < g.get_size(); i++)
	{
		for (int j = 0; j < g.get_size(); j++)
		{
			if (g.get_matrix()[i][j] == 1)
				k += 1;
		}
	}
	return k;
}

bool dfs(Graph& g, int* check, int i)
{
	int k = K(g,check,i);
	check[i] = 1;
	for (int j = 0; j < g.get_size(); j++)
	{
		if (g.get_matrix()[i][j] == 1 && check[j] == 0)
			dfs(g, check, j);

		if (k == g.get_size())
		{
			g.remove_edge(i, j);
			return 1;
		}
		else if (k == g.get_size() - 1)
			return 0;
	}
	return 1;
}


int main()
{
	setlocale(0, "");
	int count;
	int ver, road;
	std::fstream file("graph.txt");
	if (file)
	{
		file >> ver >> road;
		Graph g(ver);
		int x, y;
		for (int i = 0; i < road; i++)
		{
			file >> x >> y;
			g.add_edge(x - 1, y - 1);

			if (g.check_loop(x, y))
			{
				std::cout << "Graph has loops. Try again";
				return 0;
			}
		}
		g.print(g);
		if (DFS(g))
			std::cout << "It`s a tree graph.\n";
		else
		{
			std::cout << "\nIt`s not a tree graph\n\n";
			DFS(g);
			g.print(g);
			std::cout << "It`s a tree graph.\n";
		}
	}
	else std::cout << "File wasn`t opened.\n";
	return 0;
}
__________________________________
#include "Header.h"

Graph::Graph(int n)
{
	size = n;
	matrix = new int* [size];
	for (int i = 0; i < size; i++)
	{
		matrix[i] = new int[size];
		for (int j = 0; j < size; j++)
			matrix[i][j] = 0;
	}
}
Graph::~Graph()
{
	delete[] matrix;
}
int Graph::get_size()
{
	return size;
}
int** Graph::get_matrix()
{
	return matrix;
}
bool Graph::remove_edge(int line, int column)
{
	if (matrix[line][column] == 1)
	{
		matrix[line][column] = 0;
		matrix[column][line] = 0;
		return 1;
	}
	return 0;
}
std::ostream& operator<<(std::ostream& on, const Graph& gr)
{
	for (int i = 0; i < gr.size; i++)
	{
		for (int j = 0; j < gr.size; j++)
			on << gr.matrix[i][j] << ' ';
		on << '\n';
	}
	return on;
}
bool Graph::add_edge(int line, int column)
{
	if (matrix[line][column] == 0)
	{
		matrix[line][column] = 1;

		return 1;
	}
	else if (matrix[column][line] == 0)
	{
		matrix[column][line] = 1;
		return 1;
	}
	else
		return 0;
}
/*
void Graph::print(Graph& g)
{
	for (int i = 0; i < g.get_size(); i++)
	{
		for (int j = 0; j < g.get_size(); j++)
		{
			//return (std::to_string(g.get_matrix()[i][j]) + '\t');
			std::cout << g.get_matrix()[i][j] << ' ';

		}
		std::cout << '\n';
	}
	std::cout << '\n';
}
*/
void Graph::print(Graph& g)
{
	for (int i = 0; i < g.get_size(); i++)
	{
		for (int j = 0; j < g.get_size(); j++)
		{
			if (g.get_matrix()[i][j] == 1)
				std::cout << i + 1 << ' ' << j + 1;
		}
		std::cout << '\n';
	}
}

int Graph::check_loop(int line, int column)
{
	if (line == column)
		return 1;
	else return 0;
}
_________________________________
#pragma once
#include <iostream>
#include<string>
class Graph
{
	int size;
	int** matrix;
public:
	Graph() { size = 0; };
	Graph(int n);
	Graph(int** a, int n);
	~Graph();
	Graph(const Graph& gr);
	int get_size();
	int** get_matrix();
	bool add_edge(int line, int column);
	bool remove_edge(int line, int column);
	int check_loop(int n1, int n2);
	void print(Graph& gr);
	friend std::ostream& operator<<(std::ostream& on, const Graph& gr);
};
